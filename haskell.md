# Haskell 

## Data Types 

- ```data Bool = False | True```
  - ```Bool``` is the type constructor of datatype Bool and also the name of the
    type 
  - ```False``` and ```True``` are data constructors 
  - Entire statement is called a data declaration 


- Type class constraint
  - ```
    Prelude> :t (/)
    (/) :: Fractional a => a -> a -> a 
    ```
  - The type variable ```a``` must implement the Fractional type class
  - Aside: you want to use fixed precision when tracking money

- Tuples 
  - A tuple can have different types
    - ```
      Prelude> (,) 8 "Julie"
      (8, "Julie")
      ```
  - Two-tuple has nice default fucntiosn like ```fst``` and ```snd```
    - ```
      Prelude> 2 + fst (1, 2)
      3
      ``` 

- The compiler gives type class information instead of a concrete type if it is
  not declared yet
  - ```Prelude> :t 13
    13 :: Num a => a
    ```

- You can assign a type to a value
  - ```Prelude> fifteen = 15
    fifteenInt = fifteen :: Int
    ```

- Currying 
  - Nesting multiple functions 
  - ```(->)``` is an infix operator and is right associative:
    - ```
      f :: a -> a -> 

      -- associates to 

      f :: a -> (a -> a)
      ```
  - Partial Application 
    - A strategy to use currying to apply only part of a function:
      - ```
        addStuff :: Integer -> Integer -> Integer
        addStuff :: a b = a + b + 5

        addTen :: Integer -> Integer 
        addTen = addStuff + 5 

        -- Note:

        addStuff :: Integer -> Integer -> Integer

  
       -- is equal to 

        addStuff :: Integer -> (Integer -> Integer)
      ```
     - Sectioning - partial application of infix operators
      - ```
        > X = 5
        > y = (2^)
        > z = (^2)
        > y x
        > 32
        > z x
        > 25
        ```
    - Checking types of patial applications
      - ```
      > f :: a -> a -> a -> a; f = undefined
      > x :: Char; x = undefined
      > :t f x
      ```
- Polymorphism
  - Accept arguments of one type and return values of another 
  - Parametric polymorphism
    - Parameters are fully polymorhphic
  - Constrained polymorphism
    - Type class constraints on parameters
      - Decreasing flexibility but increases functionality
  - Removing constraints (making things more polymorphic)
    -``` 
      > 6 / length [1, 2, 3]
      > No instance for (Fractional Int) arising
          from a use of ‘/’
        In the expression: 6 / length [1, 2, 3]
        In an equation for ‘it’: it = 6 / length [1, 2, 3]

      > :type fromIntegral
      fromIntegral :: (Num b, Integral a) => a -> b

      > Prelude> 6 / fromIntegral (length [1, 2, 3])
      2.0
     ```

- Type Classes 
  - Main points:
    - type class defines set of functions and/or values
    - types have instances of that type class
    - instances specify ways that type uses the functions of the type class
  - kind of like 'interfaces' in other languages  
  - Partial functions - the dangers of 
    - ```
      f:: Int -> Bool
      f 2 = True
    ```
      - This will blow up since it can only handle a single input: 2
    - Turn all warnings in ghci to prevent partial functions:
      - ```> :set -Wall```
