<!--
## Data Types
-->

## Types de données

<!--
Every value in Rust is of a certain *data type*, which tells Rust what kind of
data is being specified so it knows how to work with that data. We’ll look at
two data type subsets: scalar and compound.
-->

Toutes les valeurs en Rust sont d'un certain *type*, qui indique à Rust quels
type de donnée est en train d'être spécifié afin qu'il puisse savoir comment
traiter la donnée. Dans cette section, nous allons nous intéresser à certains
types de données inclus dans langage. Nous divisions habituellement chaque type
dans deux catégories : les scalaires et les composés.

<!--
Keep in mind that Rust is a *statically typed* language, which means that it
must know the types of all variables at compile time. The compiler can usually
infer what type we want to use based on the value and how we use it. In cases
when many types are possible, such as when we converted a `String` to a numeric
type using `parse` in the [“Comparing the Guess to the Secret
Number”][comparing-the-guess-to-the-secret-number]<!-- ignore -- > section in
Chapter 2, we must add a type annotation, like this:
-->

Tout au long de cette section, gardez à l'esprit que Rust est langage
*statiquement typé*, ce qui signifie qu'il doit connaître les types de toutes
les variables lors de la compilation. Le compilateur peut souvent déduire quel
type utiliser en se basant sur la valeur et comment elle est utilisée. Dans les
cas où plusieurs types sont envisageables, comme lorsque nous avons converti
une `String` en un type numérique en utilisant `parse` dans le Chapitre 2, nous
devons ajouter une annotation de type, comme ceci :

<!--
```rust
let guess: u32 = "42".parse().expect("Not a number!");
```
-->

```rust
let guess: u32 = "42".parse().expect("Not a number!");
```

<!--
If we don’t add the type annotation here, Rust will display the following
error, which means the compiler needs more information from us to know which
type we want to use:
-->

Si nous n'ajoutons pas l'annotation de type ici, Rust affichera l'erreur
suivante, signifiant que le compilateur a besoin de plus d'informations pour
déterminer quel type nous souhaitons utiliser :

<!--
```text
error[E0282]: type annotations needed
 -- > src/main.rs:2:9
  |
2 |     let guess = "42".parse().expect("Not a number!");
  |         ^^^^^
  |         |
  |         cannot infer type for `_`
  |         consider giving `guess` a type
```
-->

```text
error[E0282]: type annotations needed
 --> src/main.rs:2:9
  |
2 |     let guess = "42".parse().expect("Not a number!");
  |         ^^^^^
  |         |
  |         cannot infer type for `_`
  |         consider giving `guess` a type
```

<!--
You’ll see different type annotations for other data types.
-->

Vous découvrirez différentes annotations de type au fur et à mesure que nous
discuterons des nombreux types de données.

<!--
### Scalar Types
-->

### Types scalaires

<!--
A *scalar* type represents a single value. Rust has four primary scalar types:
integers, floating-point numbers, Booleans, and characters. You may recognize
these from other programming languages. Let’s jump into how they work in Rust.
-->

Un type *scalaire* représente une seule valeur. Rust possède quatre types
scalaires principaux : les entiers, les nombres à virgule flottante, les
Booléens et les caractères. Vous les reconnaîtrez surement d'autres langages de
programmation, mais allons voir comment ils fonctionnent en Rust.

<!--
#### Integer Types
-->

#### Types entiers

<!--
An *integer* is a number without a fractional component. We used one integer
type in Chapter 2, the `u32` type. This type declaration indicates that the
value it’s associated with should be an unsigned integer (signed integer types
start with `i`, instead of `u`) that takes up 32 bits of space. Table 3-1 shows
the built-in integer types in Rust. Each variant in the Signed and Unsigned
columns (for example, `i16`) can be used to declare the type of an integer
value.
-->

Un *entier* est un nombre sans partie décimale. Nous avons utilisé un entier
plus tôt dans ce chapitre, le type `u32`. Cette déclaration de type indique 
que la valeur à laquelle elle est associée doit être un entier non signé
prenant 32 bits d'espace mémoire (le u de `u32` étant un raccourci pour
*unsigned*, "non signé", au contraire du `i32` pouvant prendre des valeurs 
négatives, le i signifiant simplement *integer*, "entier"). Le Tableau 3-1 
montre les types d'entiers inclus dans le langage. Chaque variante dans les
colonnes "Signé" et "Non Signé" (par exemple, *i16*) peut être utilisé pour
déclarer le type d'une valeur entière.

<!--
<span class="caption">Table 3-1: Integer Types in Rust</span>
-->

<span class="caption">Tableau 3-1: Les types d'entier en Rust</span>

<!--
| Length  | Signed  | Unsigned |
|---------|---------|----------|
| 8-bit   | `i8`    | `u8`     |
| 16-bit  | `i16`   | `u16`    |
| 32-bit  | `i32`   | `u32`    |
| 64-bit  | `i64`   | `u64`    |
| 128-bit | `i128`  | `u128`   |
| arch    | `isize` | `usize`  |
-->

| Taille | Signé  | Non signé |
|--------|--------|-----------|
| 8-bit  | i8     | u8        |
| 16-bit | i16    | u16       |
| 32-bit | i32    | u32       |
| 64-bit | i64    | u64       |
| arch   | isize  | usize     |

<!--
Each variant can be either signed or unsigned and has an explicit size.
*Signed* and *unsigned* refer to whether it’s possible for the number to be
negative or positive—in other words, whether the number needs to have a sign
with it (signed) or whether it will only ever be positive and can therefore be
represented without a sign (unsigned). It’s like writing numbers on paper: when
the sign matters, a number is shown with a plus sign or a minus sign; however,
when it’s safe to assume the number is positive, it’s shown with no sign.
Signed numbers are stored using [two’s complement](https://en.wikipedia.org/wiki/Two%27s_complement) representation.
-->

Chaque variante peut-être signée ou non-signée et possède une taille explicite.
Signée et non-signée indique s'il est possible ou non d'être négatif ou positif
; en d'autres termes, si l'on peut lui attribuer un signe (signé) ou s'il sera
toujours positif et que l'on peut donc le représenter sans un signe
(non-signé). C'est comme écrire des nombres sur le papier : quand le signe
importe, un nombre est écrit avec un signe plus ou un signe moins ; en
revanche, quand on peut supposer que le nombre est positif, il est écrit sans
son signe. Les nombres signés sont stockés en utilisant le complément à deux
(si vous n'êtes pas sûr de ce qu'est le complément à deux, vous pouvez le
rechercher sur internet ; une telle explication ne fait pas partie de
l'objectif de ce livre).

<!--
Each signed variant can store numbers from -(2<sup>n - 1</sup>) to 2<sup>n -
1</sup> - 1 inclusive, where *n* is the number of bits that variant uses. So an
`i8` can store numbers from -(2<sup>7</sup>) to 2<sup>7</sup> - 1, which equals
-128 to 127. Unsigned variants can store numbers from 0 to 2<sup>n</sup> - 1,
so a `u8` can store numbers from 0 to 2<sup>8</sup> - 1, which equals 0 to 255.
-->

Chaque variante signée peut stocker des nombres allant de -(2<sup>n - 1</sup>)
à 2<sup>n - 1</sup> - 1 inclus, où `n` est le nombre de bits que cette variante
utilise. Un `i8` peut donc stocker des nombres allant de -(2<sup>7</sup>) à
2<sup>7</sup> - 1, ce qui est égal à -128 jusqu'à 127.  Les variantes non
signées pouvant aller de 0 à 2<sup>n</sup> - 1, un `u8` peut donc stocker des
nombres allant de 0 à 2<sup>8</sup> - 1, ce qui équivaut à 0 jusqu'à 255.

<!--
Additionally, the `isize` and `usize` types depend on the kind of computer your
program is running on: 64 bits if you’re on a 64-bit architecture and 32 bits
if you’re on a 32-bit architecture.
-->

De plus, les types `isize` et `usize` dépendent du type d'ordinateur sur lequel
votre programme va s'exécuter: 64-bits si vous utilisez une architecture 64-bit
ou 32-bits si vous utilisez une architecture 32-bit.

<!--
You can write integer literals in any of the forms shown in Table 3-2. Note
that all number literals except the byte literal allow a type suffix, such as
`57u8`, and `_` as a visual separator, such as `1_000`.
-->

Vous pouvez écrire des nombres entiers littérals dans chacune des formes décrites dans le Tableau 3-2. Notez que chaque nombre littéral excepté l'octet accepte un suffixe de type, comme `57u8`, et `_` comme séparateur visuel, par exemple `1_000`.

<!--
<span class="caption">Table 3-2: Integer Literals in Rust</span>
-->

<span class="caption">Tableau 3-2: Les Entiers Littérals en Rust</span>

<!--
| Number literals  | Example       |
|------------------|---------------|
| Decimal          | `98_222`      |
| Hex              | `0xff`        |
| Octal            | `0o77`        |
| Binary           | `0b1111_0000` |
| Byte (`u8` only) | `b'A'`        |
-->

| Nombre litéral         | Exemple       |
|------------------------|---------------|
| Décimal                | `98_222`      |
| Hexadécimal            | `0xff`        |
| Octal                  | `0o77`        |
| Binaire                | `0b1111_0000` |
| Octet (`u8` seulement) | `b'A'`        |

<!--
So how do you know which type of integer to use? If you’re unsure, Rust’s
defaults are generally good choices, and integer types default to `i32`: this
type is generally the fastest, even on 64-bit systems. The primary situation in
which you’d use `isize` or `usize` is when indexing some sort of collection.
-->

Comment pouvez-vous déterminer le type d'entier à utiliser? Si vous n'êtes pas
sûr, les choix par défaut de Rust sont généralement de bons choix, et le type
d'entier par défaut est `i32` : c'est souvent le plus rapide, même sur des
systèmes 64-bit. La principale raison pour laquelle on utilise un `isize` ou un
`usize` serait lorsque que l'on indexe une quelconque collection.

<!--
> ##### Integer Overflow
>
> Let’s say you have a variable of type `u8` that can hold values between 0 and 255.
> If you try to change the variable to a value outside of that range, such
> as 256, *integer overflow* will occur. Rust has some interesting rules
> involving this behavior. When you’re compiling in debug mode, Rust includes
> checks for integer overflow that cause your program to *panic* at runtime if
> this behavior occurs. Rust uses the term panicking when a program exits with
> an error; we’ll discuss panics in more depth in the [“Unrecoverable Errors
> with `panic!`”][unrecoverable-errors-with-panic]<!-- ignore -- > section in
> Chapter 9.
>
> When you’re compiling in release mode with the `--release` flag, Rust does
> *not* include checks for integer overflow that cause panics. Instead, if
> overflow occurs, Rust performs *two’s complement wrapping*. In short, values
> greater than the maximum value the type can hold “wrap around” to the minimum
> of the values the type can hold. In the case of a `u8`, 256 becomes 0, 257
> becomes 1, and so on. The program won’t panic, but the variable will have a
> value that probably isn’t what you were expecting it to have. Relying on
> integer overflow’s wrapping behavior is considered an error. If you want to
> wrap explicitly, you can use the standard library type [`Wrapping`][wrapping].
-->

<!--
#### Floating-Point Types
-->

#### Types à Virgule Flottante

<!--
Rust also has two primitive types for *floating-point numbers*, which are
numbers with decimal points. Rust’s floating-point types are `f32` and `f64`,
which are 32 bits and 64 bits in size, respectively. The default type is `f64`
because on modern CPUs it’s roughly the same speed as `f32` but is capable of
more precision.
-->

Rust possède également deux types primitifs pour les *nombres à virgule
flottante*, les nombres à virgule. Les types à virgule flottante de Rust sont
les `f32` et les `f64`, qui ont respectivement une taille de 32 bits et 64
bits. Le type par défaut est le `f64` car sur nos processeurs modernes un tel
type est quasiment aussi rapide qu'un `f32` mais est capable d'une plus grande
précision.

<!--
Here’s an example that shows floating-point numbers in action:
-->

Voici un exemple montrant un nombre à virgule flottante en action :

<!--
<span class="filename">Filename: src/main.rs</span>
-->

<span class="filename">Ficher: src/main.rs</span>

```rust
fn main() {
    let x = 2.0; // f64

    let y: f32 = 3.0; // f32
}
```

<!--
Floating-point numbers are represented according to the IEEE-754 standard. The
`f32` type is a single-precision float, and `f64` has double precision.
-->

Les nombres à virgule flottante sont représentés en accord avec le standard
IEEE-754. Le type `f32` est un *float* à simple précision, et le `f64` est à
double précision.

<!--
#### Numeric Operations
-->

<!--
Rust supports the basic mathematical operations you’d expect for all of the
number types: addition, subtraction, multiplication, division, and remainder.
The following code shows how you’d use each one in a `let` statement:
-->

<!--
<span class="filename">Filename: src/main.rs</span>
-->

<!--
```rust
fn main() {
    // addition
    let sum = 5 + 10;

    // subtraction
    let difference = 95.5 - 4.3;

    // multiplication
    let product = 4 * 30;

    // division
    let quotient = 56.7 / 32.2;

    // remainder
    let remainder = 43 % 5;
}
```
-->

<!--
Each expression in these statements uses a mathematical operator and evaluates
to a single value, which is then bound to a variable. Appendix B contains a
list of all operators that Rust provides.
-->

<!--
#### The Boolean Type
-->

<!--
As in most other programming languages, a Boolean type in Rust has two possible
values: `true` and `false`. Booleans are one byte in size. The Boolean type in
Rust is specified using `bool`. For example:
-->

<!--
<span class="filename">Filename: src/main.rs</span>
-->

<!--
```rust
fn main() {
    let t = true;

    let f: bool = false; // with explicit type annotation
}
```
-->

<!--
The main way to use Boolean values is through conditionals, such as an `if`
expression. We’ll cover how `if` expressions work in Rust in the [“Control
Flow”][control-flow]<!-- ignore -- > section.
-->

<!--
#### The Character Type
-->

<!--
So far we’ve worked only with numbers, but Rust supports letters too. Rust’s
`char` type is the language’s most primitive alphabetic type, and the following
code shows one way to use it. (Note that `char` literals are specified with
single quotes, as opposed to string literals, which use double quotes.)
-->

<!--
<span class="filename">Filename: src/main.rs</span>
-->

<!--
```rust
fn main() {
    let c = 'z';
    let z = 'ℤ';
    let heart_eyed_cat = '😻';
}
```
-->

<!--
Rust’s `char` type is four bytes in size and represents a Unicode Scalar Value,
which means it can represent a lot more than just ASCII. Accented letters;
Chinese, Japanese, and Korean characters; emoji; and zero-width spaces are all
valid `char` values in Rust. Unicode Scalar Values range from `U+0000` to
`U+D7FF` and `U+E000` to `U+10FFFF` inclusive. However, a “character” isn’t
really a concept in Unicode, so your human intuition for what a “character” is
may not match up with what a `char` is in Rust. We’ll discuss this topic in
detail in [“Storing UTF-8 Encoded Text with Strings”][strings]<!-- ignore -- >
in Chapter 8.
-->

<!--
### Compound Types
-->

<!--
*Compound types* can group multiple values into one type. Rust has two
primitive compound types: tuples and arrays.
-->

<!--
#### The Tuple Type
-->

<!--
A tuple is a general way of grouping together some number of other values
with a variety of types into one compound type. Tuples have a fixed length:
once declared, they cannot grow or shrink in size.
-->

<!--
We create a tuple by writing a comma-separated list of values inside
parentheses. Each position in the tuple has a type, and the types of the
different values in the tuple don’t have to be the same. We’ve added optional
type annotations in this example:
-->

<!--
<span class="filename">Filename: src/main.rs</span>
-->

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

<!--
The variable `tup` binds to the entire tuple, because a tuple is considered a
single compound element. To get the individual values out of a tuple, we can
use pattern matching to destructure a tuple value, like this:
-->

<!--
<span class="filename">Filename: src/main.rs</span>
-->

<!--
```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {}", y);
}
```
-->

<!--
This program first creates a tuple and binds it to the variable `tup`. It then
uses a pattern with `let` to take `tup` and turn it into three separate
variables, `x`, `y`, and `z`. This is called *destructuring*, because it breaks
the single tuple into three parts. Finally, the program prints the value of
`y`, which is `6.4`.
-->

<!--
In addition to destructuring through pattern matching, we can access a tuple
element directly by using a period (`.`) followed by the index of the value we
want to access. For example:
-->

<!--
<span class="filename">Filename: src/main.rs</span>
-->

<!--
```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```
-->

<!--
This program creates a tuple, `x`, and then makes new variables for each
element by using their index. As with most programming languages, the first
index in a tuple is 0.
-->

<!--
#### The Array Type
-->

<!--
Another way to have a collection of multiple values is with an *array*. Unlike
a tuple, every element of an array must have the same type. Arrays in Rust are
different from arrays in some other languages because arrays in Rust have a
fixed length, like tuples.
-->

<!--
In Rust, the values going into an array are written as a comma-separated list
inside square brackets:
-->

<!--
<span class="filename">Filename: src/main.rs</span>
-->

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
}
```

<!--
Arrays are useful when you want your data allocated on the stack rather than
the heap (we will discuss the stack and the heap more in Chapter 4) or when
you want to ensure you always have a fixed number of elements. An array isn’t
as flexible as the vector type, though. A vector is a similar collection type
provided by the standard library that *is* allowed to grow or shrink in size.
If you’re unsure whether to use an array or a vector, you should probably use a
vector. Chapter 8 discusses vectors in more detail.
-->

<!--
An example of when you might want to use an array rather than a vector is in a
program that needs to know the names of the months of the year. It’s very
unlikely that such a program will need to add or remove months, so you can use
an array because you know it will always contain 12 items:
-->

<!--
```rust
let months = ["January", "February", "March", "April", "May", "June", "July",
              "August", "September", "October", "November", "December"];
```
-->

<!--
You would write an array’s type by using square brackets, and within the
brackets include the type of each element, a semicolon, and then the number of
elements in the array, like so:
-->

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

<!--
Here, `i32` is the type of each element. After the semicolon, the number `5`
indicates the element contains five items.
-->

<!--
Writing an array’s type this way looks similar to an alternative syntax for
initializing an array: if you want to create an array that contains the same
value for each element, you can specify the initial value, followed by a
semicolon, and then the length of the array in square brackets, as shown here:
-->

```rust
let a = [3; 5];
```

<!--
The array named `a` will contain `5` elements that will all be set to the value
`3` initially. This is the same as writing `let a = [3, 3, 3, 3, 3];` but in a
more concise way.
-->

<!--
##### Accessing Array Elements
-->

<!--
An array is a single chunk of memory allocated on the stack. You can access
elements of an array using indexing, like this:
-->

<!--
<span class="filename">Filename: src/main.rs</span>
-->

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```

<!--
In this example, the variable named `first` will get the value `1`, because
that is the value at index `[0]` in the array. The variable named `second` will
get the value `2` from index `[1]` in the array.
-->

<!--
##### Invalid Array Element Access
-->

<!--
What happens if you try to access an element of an array that is past the end
of the array? Say you change the example to the following code, which will
compile but exit with an error when it runs:
-->

<!--
<span class="filename">Filename: src/main.rs</span>
-->

<!--
```rust,ignore,panics
fn main() {
    let a = [1, 2, 3, 4, 5];
    let index = 10;

    let element = a[index];

    println!("The value of element is: {}", element);
}
```
-->

<!--
Running this code using `cargo run` produces the following result:
-->

```text
$ cargo run
   Compiling arrays v0.1.0 (file:///projects/arrays)
    Finished dev [unoptimized + debuginfo] target(s) in 0.31 secs
     Running `target/debug/arrays`
thread 'main' panicked at 'index out of bounds: the len is 5 but the index is
 10', src/main.rs:5:19
note: Run with `RUST_BACKTRACE=1` for a backtrace.
```

<!--
The compilation didn’t produce any errors, but the program resulted in a
*runtime* error and didn’t exit successfully. When you attempt to access an
element using indexing, Rust will check that the index you’ve specified is less
than the array length. If the index is greater than or equal to the array
length, Rust will panic.
-->

<!--
This is the first example of Rust’s safety principles in action. In many
low-level languages, this kind of check is not done, and when you provide an
incorrect index, invalid memory can be accessed. Rust protects you against this
kind of error by immediately exiting instead of allowing the memory access and
continuing. Chapter 9 discusses more of Rust’s error handling.
-->

[comparing-the-guess-to-the-secret-number]:
ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[control-flow]: ch03-05-control-flow.html#control-flow
[strings]: ch08-02-strings.html#storing-utf-8-encoded-text-with-strings
[unrecoverable-errors-with-panic]: ch09-01-unrecoverable-errors-with-panic.html
[wrapping]: ../std/num/struct.Wrapping.html
