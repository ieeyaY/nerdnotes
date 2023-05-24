# Julia

[[TOC]]

## Variable

特殊变量 (build-in): `pi, \pi,` 内置函数
L-Value: `___`

## Integer & Float

Real

```txt
Number
 ├─ Complex
 └─ Real
     ├─ AbstractFloat
     │   ├─ BigFloat
     │   ├─ Float16        │ half
     │   ├─ Float32        │ single
     │   └─ Float64        │ double
     ├─ AbstractIrrational
     │   └─ Irrational
     ├─ Integer
     │   ├─ Bool
     │   ├─ Signed
     │   │   ├─ BigInt
     │   │   ├─ Int128
     │   │   ├─ Int16      │ Int
     │   │   ├─ Int32      │
     │   │   ├─ Int64      │
     │   │   └─ Int8       │
     │   └─ Unsigned
     │       ├─ UInt128
     │       ├─ UInt16     │ UInt
     │       ├─ UInt32     │
     │       ├─ UInt64     │
     │       └─ UInt8      │
     └─ Rational
```

`Sys.WORD_SIZE` 操作系统字长
`typeof(x)` 变量类型
`typemax(T), typemin(T)` real 类型最大最小值, T:
    - variable, max|min of variable type
    - Type{T}, max|min of type T

### Integer

`0b000` bin, `0x000` hex, `big(10)` big

### Float

`1.0e10` Float64, `1.0f10` Float32
`bitstring(0.0)` float bitstring
`eps()` machine epsilon (`prevfloat(), nextfloat()`)

#### Special Float

| Float16 | Float32 | Float64 |
| ---     | ---     | ---     |
| Inf16   | Inf32   | Inf     |
| -Inf16  | -Inf32  | -Inf    |
| NaN16   | NaN32   | NaN     |

### Arbitrary Precision Arithmetic

```julia
@big_str "123456"
BigInt(123456)
big"123456"
parse(BigInt, "123456") # or BigFloat, etc.
```

### Numberic Literal Coefficients

`2*x + 1` = `2x + 1`
precedence is HIGHTER than other operators

### `one(x)` `zero(x)`

Literal one or zero of type or variable x

## Math

### Operator

#### Special operators form other language

```julia
x ÷ y == x / y  # ÷ is \div
x \ y == y / x
```

#### When used in multiplication, false acts as a strong zero

```julia
NaN * false # is 0
false * Inf # is 0
```

#### Boolean

`!x`, `x && y`, `x || y`   (short-circuiting)

#### Bitwise

`~x`, `x & y`, `x | y`, ...

#### Operator: =

`+= -= *= /= \= ÷= %= ^= &= |= ⊻= >>>= >>= <<=`

#### dot

`a .^ b` parsed as `(^).(a, b)`
marco format:
`@. 2*A^2 + sin(A)`

### Comparision

`== != ≠ <  > <= >= ≥ ≤ # \ne \ge, \le`
`NaN != NaN` other comparisions are False

Compare functions:

```julia
isequal(x) # consider NaN as euqual, no matter bits
isfinite(x)
isinf(x)
isnan(x)
```

Chaining Comparisons `1 < 2 <= 2 < 3 == 3 > 2 >= 1 == 1 < 3 != 5` is short-circuiting

### Numberical Conversions

```julia
T(x), convert(T, x)
x % T   # T <: Integer
round(x)
round(T, x)
floor, ceil, trunc
```

[Rounding-functions](https://docs.julialang.org/en/v1/manual/mathematical-operations/#Rounding-functions)
[Division functions](https://docs.julialang.org/en/v1/manual/mathematical-operations/#Division-functions)
[Sign and absolute value functions](https://docs.julialang.org/en/v1/manual/mathematical-operations/#Sign-and-absolute-value-functions)
[Powers, logs and roots](https://docs.julialang.org/en/v1/manual/mathematical-operations/#Powers,-logs-and-roots)
[Special functions](https://github.com/JuliaMath/SpecialFunctions.jl)

## Complex & Rational Numbers

### Complex

```julia
C = 1 + 2im
real(C)           # 1
imag(C)           # 2
conj(C)           # 1 - 2im
abs(C)            # 2.236 (sqrt(5))
abs2(C)           # 5
angle(C)          # phase angle in radians

sqrt(-1)          # DomainError
sqrt(Complex(-1)) # 1im
```

### Rational

```julia
numerator(1//2)   # 1
denominator(1//2) # 2
```

## String

### `Char`

```julia
c = Int('x')    # 120
Char(120)       # 'x'
```

> Unicode Input
> | script          | format              |
> | `\bf[a-zA-Z]`   | Bold                |
> | `\it[a-zA-Z]`   | Italic              |
> | `\bi[a-zA-Z]`   | Bold Italic         |
> | `\scr[a-zA-Z]`  | Mathematical Script |
> | `\bscr[a-zA-Z]` | Bold Math Script    |

### `String`

```julia
str = "abc"
multiLine = """Contains "quote" characters"""
longLine = "This is a long \
            line"               # This is a long line"
str[begin] == str[1]
str[end]
str[end-1]
str[end/2]
str[begin:end]
str[1]          # 'H'
str[1:1]        # "H"
SubString(str, 1, 4) == str[1:4]
```

Some index function
`firstindex(x)` `lastindex(x)` `eachindex(x)`

Some collection function (iterable)

```julia
collection(element_type, collection)
collection(collection)

foreach(f, c...)
```

### Concatenation

```julia
string(str1, ", ", str2)
str1 * ", " * str2
```

> useful functions
> `string(n::Integer; base::Integer = 10, pad::Integer = 1)` convert `n` to string
> `string(xs ...)` use `print` function to convert xs to string

### Interpolation

```julia
"$var1, $var2"
"expr = $(expr)"
```

### Common Operators

`<` `>` `==`

```julia
findfirst('o', "xylophone")     # 4
findfirst("o", "xylophone")     # 4:4

occursin("o", "Xylophon")   # true, also for 'o'

repeat("a", 10)     # "aaaaaaaaaa", also for 'a'
join(str1, str2)
join(["apples", "bananas", "pineapples"], ", ", " and ")
# "apples, bananas and pineapples"
# join str1 with str2...
```

> useful functions
> `firstindex(str)` gives the minimal (byte) index that can be used to index into `str` (always 1 for strings, not necessarily true for other containers).
> `lastindex(str)` gives the maximal (byte) index that can be used to index into `str`.
> `length(str)` the number of characters in `str`.
> `length(str, i, j)` the number of valid character indices in `str` from `i` to `j`.
> `ncodeunits(str)` number of code units in a string.
> `codeunit(str, i)` gives the code unit value in the string `str` at index `i`.
> `thisind(str, i)` given an arbitrary index into a string find the first index of the character into which the index points.
> `nextind(str, i, n=1)` find the start of the nth character starting after index `i`.
> `prevind(str, i, n=1)` find the start of the nth character starting before index `i`.

### Regex

```julia
r"regex"
occursin(r"^\s*(?:#|$)", "# a comment") # true

m = match(r"nocap (cap1) (?<g>cap2)", "xxx nocap cap1 cap2")
# RegexMatch("nocap cap1 cap2", 1="cap1", g="cap2")
m.regex     # r"nocap (cap1) (?<g>cap2)"
m.match     # "nocap cap1 cap2"
m.captures  # Union{Nothing, SubString{String}}["cap1", "cap2"]
m.offset    # 5         offset of nocapture
m.offsets   # [11, 16]  offsets of captures
```

> useful functions
> `fieldnames(x::DataType)` Return (:fieldname1, :fieldname2, :fieldname3)
> `replace(A, old_new::Pair, [count::Integer])`
> `replace("first second", r"(\w+) (?<agroup>\w+)" => s"\g<agroup> \1")`

perlre modes
`r"regex"imsx`

- i ignore cases
- m treat as multi-line
- s treat as single-line
- x allow ' ' to loose regex, use '\s' to indicate actual ' '

### Byte Array Literals

`b"..."`

### Raw String Leterals

## Functions

Typically, julia functions use "pass-by-sharing"

Declare arguments types.

```julia
function g(x::Integer, y::Integer)::Int8
    ...
end
```

### The `return` Keyword

return `return` expr, if no `return`: return last expr
display last expr
return `nothing`: `return nothing`

### Operator functions

| Expression | Calls |
| --- | --- |
| `[A B C ...]` | `hcat` |
|`[A; B; C; ...]`| `vcat` |
|`[A B; C D; ...]`| `hvcat` |
| `A'` | `adjoint` |
| `A[i]` | `getindex` |
| `A[i] = ai` | `setindex!` |
| `A.n` | `getproperty` |
| `A.n = an` | `setproperty!` |

### Anonymous Function

```julia
x -> x^2 + x + 1
(x,y,z) -> 2x + y - 1
() -> π               # use for delay a computation
#delay computation example:
get(dict, key) do
  time()
end
# equals to
get(()->time(), dict, key)

map(x -> x^2, X)
```

> Keywords
> `do` Create an anonymous function and pass it as the first argument to a function call.
>
> ```julia
> map(iter) do i
>   <expr>
> end
> ```
>
> equals to `map(i -> <expr>, iter)`

> Useful macro
> `@show`

