# Haskell Examples



## Reading Values 

```haskell
data Name = Name { firstName :: String, lastName :: String }
main = do 
      let tim = Name "tim" "lim"
      putStrLn (firstName tim)

```

or with a sum type:

```haskell
data Name = Name FirstName LastName 
					| NameMiddle FirstName Middle LastName

main = do 
      let Name fn _ = Name "tim" "lim"
      putStrLn fn
```

[Further reading](https://stackoverflow.com/questions/58077656/access-data-property-haskell#58077750)



## Reading a YAML file

```haskell
{-# LANGUAGE DeriveGeneric #-}

import GHC.Generics
import Data.Yaml
import Data.HashMap.Strict

data Config = Config { 
    callbackRequests :: (HashMap String String) 
  } deriving (Show, Generic)

instance FromJSON Config

main :: IO ()
main = do
  file <- decodeFile "config.yaml" :: IO (Maybe Config)
  putStrLn (maybe "Error reading file" (show . callbackRequests) file)

```



## Simple STM Example

```haskell
module Main where

import Control.Concurrent.STM
import qualified Data.HashMap.Strict as Map

data State = State { 
    callbackRequests :: Map.HashMap String String
  } deriving (Show)

type MyAppState = TVar State

initState :: Map.HashMap String String -> STM MyAppState 
initState m = newTVar $ State $ m

addToState :: (String, String) -> State -> State
addToState (k, v) s = State $ Map.insert k v $ callbackRequests s

main :: IO ()
main =  
  do 
    state <- atomically $ initState $ Map.fromList [("hi", "bye")]
    stateToPrint <- readTVarIO state
    putStrLn (show stateToPrint)
    atomically (readTVar state >>= writeTVar state . (addToState ("foo", "bar")))
    stateToPrint <- readTVarIO state
    putStrLn (show stateToPrint)
```



## Bank STM Example

```haskell
import Control.Concurrent
import Control.Concurrent.MVar
import Control.Concurrent.STM
import Control.Monad
import System.Random

import qualified Data.Map as Map

type AccountId = Int
type Account = TVar Dollars
type Dollars = Integer
type Bank = TVar (Map.Map AccountId Account)

numberOfAccounts = 20
threads = 100
transactionsPerThread = 100
maxAmount = 1000

-- Get account by ID, create new empty account if it didn't exist
getAccount :: Bank -> AccountId -> STM Account
getAccount bank accountId = do
  accounts <- readTVar bank
  case Map.lookup accountId accounts of
    Just account -> return account
    Nothing -> do
      account <- newTVar 0
      writeTVar bank $ Map.insert accountId account accounts
      return account

-- Transfer amount between two accounts (accounts can go negative)
transfer :: Dollars -> Account -> Account -> STM ()
transfer amount from to = when (from /= to) $ do
  balanceFrom <- readTVar from
  balanceTo <- readTVar to
  writeTVar from $! balanceFrom - amount
  writeTVar to $! balanceTo + amount

randomTransaction :: Bank -> IO ()
randomTransaction bank = do
  -- Make a random transaction
  fromId <- randomRIO (1, numberOfAccounts)
  toId   <- randomRIO (1, numberOfAccounts)
  amount <- randomRIO (1, maxAmount)

  -- Perform it atomically
  atomically $ do
    from <- getAccount bank fromId
    to   <- getAccount bank toId
    transfer amount from to

main = do
  bank <- newTVarIO Map.empty

  -- Start some worker threads to each do a number of random transactions
  workers <- replicateM threads $ do
    done <- newEmptyMVar
    forkIO $ do
      replicateM_ transactionsPerThread $ randomTransaction bank
      putMVar done ()
    return done

  -- Wait for worker threads to finish
  mapM_ takeMVar workers

  -- Print list of accounts and total bank balance (which should be zero)
  summary <- atomically $ do
    accounts <- readTVar bank
    forM (Map.assocs accounts) $ \(accountId, account) -> do
      balance <- readTVar account
      return (accountId, balance)

  mapM_ print summary
  putStrLn "----------------"
  putStrLn $ "TOTAL BALANCE: " ++ show (sum $ map snd summary)
```

