# Notes on The Haskell Language

## Type Basics

You can desugar a multiargument function like this:

```haskell
makeAddress :: Int -> String -> String -> (Int, String, String)
makeAddress number stree town = (number, street, town)

makeAddressLambda = (\number -> 
				(\street -> 
				  \town -> (number, street, town)))
```

### Creating New Types 

Type synonyms can clarify code:

```haskell
type FirstName = String
type LastName = String 
type PatientName = (FirstName, LastName)

firstName :: PatientName -> String
firstName patient = fst patient
```

Defining your own type:

```haskell
data Sex = Male | Female

-- Now we use it
sexInitial :: Sex -> Char
sexInitial Male = 'M'
sexInitial Femail = 'F'
```

Things are clearer with record syntax.

Let's define a Patient data type:

```Haskell
data Patient = Patient Name Sex Int Int Int BloodType
```

Which can be defined with record syntax:

```haskell
data Patient = Patient { name :: Name
                       , sex :: Sex
                       , age :: Int
                       , height :: Int
                       , weight :: Int
                       , bloodType :: BloodType }
```

And then an actual patient:

```haskell
jackieSmith :: Patient
jackieSmith = Patient {name = Name "Jackie" "Smith"
                      , age = 43
                      , sex = Female
                      , height = 62
                      , weight = 115
                      , bloodType = BloodType O Neg }
```

```bash
GHCi> height jackieSmith
62
```

You can update with record syntax too:

```haskell
jackieSmithUpdated = jackieSmith { age = 44 }
```

Helper function to print to console:

```haskell
showSex Male = "Male"
showSex Female = "Female"

patientSummary :: Patient -> String
patientSummary patient = "**************\n" ++
                         "Sex: " ++ showSex (sex patient) ++ "\n" ++
                         "Age: " ++ show (age patient) ++ "\n" ++
                         "Height: " ++ show (height patient) ++ " in.\n" ++
                         "Weight: " ++ show (weight patient) ++ " lbs.\n" ++
                         "Blood Type: " ++ showBloodType (bloodType patient) ++
                         "\n**************\n"
```

## Type Classes


Type class overview

![img](https://dpzbhybb2pdcj.cloudfront.net/kurt/Figures/14fig02_alt.jpg)



Type classes describe how different types can behave the same way. 

```haskell
class Show a where
  show :: a -> String			
```

Types that derive the typeclass ```show``` can be turned into a ```String``` and therefore can be printed:

```haskell
data Icecream = Chocolate | Vanilla deriving (Show)
```

```bash
GHCi> Chocolate
Chocolate
GHCi> Vanilla
Vanilla
```

You can derive type classes to inherit their functions. For example we can create a six-sided dice with the ```Enum``` typeclass:

```haskell
data SixSidedDie = S1 | S2 | S3 | S4 | S5 | S6 deriving (Enum)
```

```
GHCi> [S1 .. ]
[one,two,three,four,five,six
```

Sometimes you need to implement an instance of a typeclass to customise the default functionality:

```haskell
data Name = Name (String, String) deriving (Show, Eq)

-- So we can sort by surname
instance Ord Name where
   compare (Name (f1,l1)) (Name (f2,l2)) = compare (l1,f1) (l2,f2)
   
names :: [Name]
names = [Name ("Emil","Cioran")
         , Name ("Eugene","Thacker")
         , Name ("Friedrich","Nietzsche")]
```

```bash
GHCi> import Data.List
GHCi> sort names
[Name ("Emil","Cioran"),Name ("Friedrich","Nietzsche"),
Name ("Eugene","Thacker")]
```

### Creating Types with "and" and "or"

There are two ways to combine types in Haskell, with 'and' to make 'product types' and 'or' to make 'sum types'.

Let's make a book with 'and' using record syntax:

```haskell
data AuthorName = AuthorName {
     firstName :: String
   , lastName :: String
}

data ArtistName = ArtistName {
     name :: String
}

data Book = Book {
     author  		 :: AuthorName
   , recordTitle :: String
   , bookYear    :: Int}
   
data VinylRecord = VinylRecord {
     artist        :: ArtistName
   , recordTitle   :: String
   , recordYear    :: Int}
```

But you can't create a type that combines both Book and Vinyl Record.

With sum types you can:

```haskell
data Creator = AuthorCreator AuthorName | ArtistCreator ArtistName
	
data Book = Book {
     author  :: Creator
   , recordTitle :: String
   , bookYear    :: Int}
   
data VinylRecord = VinylRecord {
     artist        :: Creator
   , recordTitle   :: String
   , recordYear    :: Int}
   
data StoreItem = BookItem Book | RecordItem VinylRecord
```

Now we can search using the powerful ```StoreItem```:

````haskell
madeBy :: StoreItem -> String
madeBy (BookItem book) = show (author book)
madeBy (RecordItem record) = show (artist record)
madeBy _ = "unknown"
````

[Further reading](https://livebook.manning.com/book/get-programming-with-haskell/chapter-16/1)



### Semigroups

You can compose functions with ```.```:

```haskell
myLast :: [a] -> a
myLast = head . reverse 		
```

You can compose like types with the semigroup method ```<>```. We can implement Semigroup for Integer like so:	

```haskell
instance Semigroup Integer where
	(<>) x y = x + y
```

### Monoids





#### misc.

```
instance Eq a => Eq (BinTree a) where
    Leaf a == Leaf b = a == b
    Branch l r == Branch l' r' = l == l' && r == r'
    _ == _ = False
```

The first line of this can be read "if `a` is an instance of `Eq`, then `BinTree a` is also an instance of `Eq`". We then provide the definitions. If we did not include the `Eq a =>` part, the compiler would complain because we're trying to use the `==` function on `a`s in the second line.

The "`Eq a =>`" part of the definition is called the "context."

[src](https://en.wikibooks.org/wiki/Yet_Another_Haskell_Tutorial/Type_advanced#Instances)