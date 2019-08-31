

# Haskell 

### Stack

Run the app: 

```stack exec app```

(where ```app``` is defined in stack.yaml)

### Snippets

Handle a maybe 

```haskell
justConfig <- decodeFile "config.yaml" :: IO (Maybe Config)
config <- (maybe (Map.fromList [("hi", "by1")]) file)
```

Using fmap ```<$>``` to read a record from a type with record syntax:

``` haskell
c <- liftIO $ config <$> (readTVarIO s)
```



### Resources

- [Cheatsheet](http://cheatsheet.codeslower.com/CheatSheet.pdf)

