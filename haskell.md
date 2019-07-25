# Haskell 

## Data Types 

- ```
  data Bool = False | True
  ```
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

- Lists 
  - Need to be of the same type





