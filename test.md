## Equational Reasoning

Commutativity: x y = y x

Associativity: x + (y + z) = (x + y) + z

Left Distributivity: x (y + z) = xy + xz

Right Distributivity: (x + y) z = xz + yz

### Reasoning with Bool
Proving not (not b) = b

    not :: Bool -> Bool
    not True = False
    not False = True

    not (not True) = not (False)
                   = True
    not (not False) = not (True)
                    = False
    => not (not b) = b

Taking cases into account, e.g. isZero

    isZero :: Int -> Bool
    isZero 0 = True   =>  isZero 0 | True   = True
    isZero n = False  =>  isZero n | n /= 0 = False

Cases need to be interpreted by conjoining the negation of the previous case guards to them.

### List Example
#### Proving reverse xs = xs for any singleton list xs

    reverse :: [a] -> [a]
    reverse [] = []
    reverse (x:xs) = reverse xs ++ [x]

    reverse [x]
    = {syntactic sugar} reverse (x : [])
    = {defn of reverse} reverse [] ++ [x]
    = {defn of reverse} [] ++ [x]
    = {defn of ++} [x]  (++) :: [a] -> [a] -> [a], [] ++ ys = ys, (x:xs) ++ ys = x : (xs ++ ys)
    => reverse [x] = [x]

However, this has only proved reverse [x] = [x] for some variable x.

The logical principle of generalisation says this is fine if there are no assumptions made about the variable x, because x can be instantiated by any value, and the equation is true for x, then the equation is true for any value.

### Structural Induction

Proof by induction uses the fact that natural numbers are a Structured Data Type.

    data Nat = Zero | Succ Nat

Proving reverse (reverse xs) = xs for any list xs

