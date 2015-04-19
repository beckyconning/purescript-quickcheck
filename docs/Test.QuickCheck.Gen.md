# Module Documentation

## Module Test.QuickCheck.Gen


This module defines the random generator monad used by the `Test.QuickCheck`
module, as well as helper functions for constructing random generators.

#### `Size`

``` purescript
type Size = Int
```

Tests are parameterized by the `Size` of the randomly-generated data,
the meaning of which depends on the particular generator used.

#### `GenState`

``` purescript
type GenState = { size :: Size, newSeed :: Seed }
```

The state of the random generator monad

#### `GenOut`

``` purescript
type GenOut a = { value :: a, state :: GenState }
```

The output of the random generator monad

#### `Gen`

``` purescript
data Gen a
```

The random generator monad

`Gen` is a state monad which encodes a linear congruential generator.

#### `repeatable`

``` purescript
repeatable :: forall a b. (a -> Gen b) -> Gen (a -> b)
```

Create a random generator for a function type.

#### `stateful`

``` purescript
stateful :: forall a. (GenState -> Gen a) -> Gen a
```

Create a random generator which uses the generator state explicitly.

#### `variant`

``` purescript
variant :: forall a. Seed -> Gen a -> Gen a
```

Modify a random generator by setting a new random seed.

#### `sized`

``` purescript
sized :: forall a. (Size -> Gen a) -> Gen a
```

Create a random generator which depends on the size parameter.

#### `resize`

``` purescript
resize :: forall a. Size -> Gen a -> Gen a
```

Modify a random generator by setting a new size parameter.

#### `choose`

``` purescript
choose :: Number -> Number -> Gen Number
```

Create a random generator which samples a range of `Number`s i
with uniform probability.

#### `chooseInt`

``` purescript
chooseInt :: Int -> Int -> Gen Int
```

Create a random generator which chooses an integer from a range.

#### `oneOf`

``` purescript
oneOf :: forall a. Gen a -> [Gen a] -> Gen a
```

Create a random generator which selects and executes a random generator from
a non-empty collection of random generators with uniform probability.

#### `frequency`

``` purescript
frequency :: forall a. Tuple Number (Gen a) -> [Tuple Number (Gen a)] -> Gen a
```

Create a random generator which selects and executes a random generator from
a non-empty, weighted collection of random generators.

#### `arrayOf`

``` purescript
arrayOf :: forall a. Gen a -> Gen [a]
```

Create a random generator which generates an array of random values.

#### `arrayOf1`

``` purescript
arrayOf1 :: forall a. Gen a -> Gen (Tuple a [a])
```

Create a random generator which generates a non-empty array of random values.

#### `vectorOf`

``` purescript
vectorOf :: forall a. Int -> Gen a -> Gen [a]
```

Create a random generator which generates a vector of random values of a specified size.

#### `elements`

``` purescript
elements :: forall a. a -> [a] -> Gen a
```

Create a random generator which selects a value from a non-empty collection with
uniform probability.

#### `runGen`

``` purescript
runGen :: forall a. Gen a -> GenState -> GenOut a
```

Run a random generator

#### `evalGen`

``` purescript
evalGen :: forall a. Gen a -> GenState -> a
```

Run a random generator, keeping only the randomly-generated result

#### `showSample'`

``` purescript
showSample' :: forall r a. (Show a) => Size -> Gen a -> Eff (console :: CONSOLE | r) Unit
```

Print a random sample to the console

#### `showSample`

``` purescript
showSample :: forall r a. (Show a) => Gen a -> Eff (console :: CONSOLE | r) Unit
```

Print a random sample of 10 values to the console

#### `uniform`

``` purescript
uniform :: Gen Number
```

A random generator which approximates a uniform random variable on `[0, 1]`

#### `perturbGen`

``` purescript
perturbGen :: forall a. Number -> Gen a -> Gen a
```

Perturb a random generator by modifying the current seed

#### `functorGen`

``` purescript
instance functorGen :: Functor Gen
```


#### `applyGen`

``` purescript
instance applyGen :: Apply Gen
```


#### `applicativeGen`

``` purescript
instance applicativeGen :: Applicative Gen
```


#### `bindGen`

``` purescript
instance bindGen :: Bind Gen
```


#### `monadGen`

``` purescript
instance monadGen :: Monad Gen
```



