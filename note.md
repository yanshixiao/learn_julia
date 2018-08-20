### 数学操作和基本函数

#### 算术操作

基本的加减乘除没什么可说的。其中`/`精确除法。而`÷`则是先进性`y/x`，然后转换成整数（向下取整）。另外`\`表示相反的除法，即分母除以分子：`x\y`等同于`y/x`。

```
julia> 1/3
0.3333333333333333

julia> 1÷3
0
```

按照惯例，用空格间隔运算符来标识优先级。如`-x + 2`标识先对x取反再对结果加2。

#### 位运算
- ~x 位求反
- x & y 按位与
- x | y 按位或
- x ⊻ y 按位异或
- x >>> y 逻辑右移
- x >> y 算术右移
- x << y 逻辑/算术左移

```
julia> ~123
-124

julia> 123 & 234
106

julia> 123 | 234
251

julia> 123 ⊻ 234
145

julia> xor(123,234)
145
```
#### 复合赋值运算符
二元算术和位运算都有对应的复合赋值运算符，即运算的结果将会被赋值给左操作数。在操作符的后面直接加上 = 就组成了复合赋值运算符。例如, `x += 3` 相当于 `x = x + 3`：

```
julia> x = 1
1

julia> x += 3
4

julia> x
4
```

复合运算符有：

```
+=  -=  *=  /=  \=  ÷=  %=  ^=  &=  |=  ⊻=  >>>=  >>=  <<=
```
#### 向量化
```
julia> [1,2,3] .^ 3
3-element Array{Int64,1}:
  1
  8
 27
```

#### 数值比较
- == 相等
- !=,≠ 不等
- < 小鱼
- <=, ≤ 小于等于
- \> 大于
- \>=, ≥ 大于等于

```julia
julia> 1 == 1
true

julia> 1 == 2
false

julia> 1 != 2
true

julia> 1 == 1.0
true

julia> 1 < 2
true

julia> 1.0 > 3
false

julia> 1 >= 1.0
true

julia> -1 <= 1
true

julia> -1 <= -1
true

julia> -1 <= -2
false

julia> 3 < -0.5
false
```

- 正数的零等于但不大于负数的零。
- `Inf` 等于他本身，并且大于所有数，除了`NaN`。
- `-Inf` 等于他本身，并且小于所有数，除了`NaN`
- `NaN` 不等于、不大于、不小于任何数，包括它本身。

```julia
julia> NaN == NaN
false

julia> NaN != NaN
true

julia> NaN < NaN
false

julia> NaN > NaN
false
```
- isequal(x, y) x 是否等价于 y
- isfinite(x)	x 是否为有限的数
- isinf(x)	x 是否为无限的数
- isnan(x)	x 是否不是数

##### 链式比较
像python一样，没啥可说的

#### 运算符优先级和结合性

#### 数字转换

##### 舍入函数
- round(x) 舍入到最近的整数
- round(T, x) 把x舍入到最近的整数

##### 除法函数

div, fld, cld, rem, divrem, mod, mod2pi, gcd, lcm等。

##### 符号函数和绝对值函数
abs, abs2, sign, signbit, copysign, flipsign等。

##### 乘方，指数和开方
sqrt, cbrt, hypot, exp, expm1, ldexp, log, log2, log10, log1p, exponent, significand等。

##### 三角和曲线函数
```
sin    cos    tan    cot    sec    csc
sinh   cosh   tanh   coth   sech   csch
asin   acos   atan   acot   asec   acsc
asinh  acosh  atanh  acoth  asech  acsch
sinc   cosc
```

### 复数和有理(分)数

#### 复数

全局变量`im`表示-1的平方根。

```julia
julia> 1 + 2im
1 + 2im
```

可以用复数进行基本算术操作

```julia
julia> (1 + 2im)*(2 - 3im)
8 + 1im

julia> (1 + 2im)/(1 - 2im)
-0.6 + 0.8im

julia> (1 + 2im) + (1 - 2im)
2 + 0im

julia> (-3 + 2im) - (5 - 1im)
-8 + 3im

julia> (-1 + 2im)^2
-3 - 4im

julia> (-1 + 2im)^2.5
2.729624464784009 - 6.9606644595719im

julia> (-1 + 2im)^(1 + 1im)
-0.27910381075826657 + 0.08708053414102428im

julia> 3(2 - 5im)
6 - 15im

julia> 3(2 - 5im)^2
-63 - 60im

julia> 3(2 - 5im)^-1.0
0.20689655172413796 + 0.5172413793103449im
```

类型提升机制保证了不同类型的运算对象能够在一起运算:

```julia
julia> 2(1 - 1im)
2 - 2im

julia> (2 + 3im) - 1
1 + 3im

julia> (1 + 2im) + 0.5
1.5 + 2.0im

julia> (2 + 3im) - 0.5im
2.0 + 2.5im

julia> 0.75(1 + 2im)
0.75 + 1.5im

julia> (2 + 3im) / 2
1.0 + 1.5im

julia> (1 - 3im) / (2 + 2im)
-0.5 - 1.0im

julia> 2im^2
-2 + 0im

julia> 1 + 3/4im
1.0 - 0.75im
```

用来处理复数的标准函数有：

```julia
julia> z = 1 + 2im
1 + 2im

julia> real(1 + 2im) # real part of z
1

julia> imag(1 + 2im) # imaginary part of z
2

julia> conj(1 + 2im) # complex conjugate of z
1 - 2im

julia> abs(1 + 2im) # absolute value of z
2.23606797749979

julia> abs2(1 + 2im) # squared absolute value
5

julia> angle(1 + 2im) # phase angle in radians
1.1071487177940904
```

通常， 复数的绝对值( abs )是它到零的距离。 函数 abs2 返回绝对值的平方， 特别地用在复数上来避免开根。angle 函数返回弧度制的相位(即 argument 或 arg )。 所有的基本函数也可以应用在复数上：

```julia
julia> sqrt(1im)
0.7071067811865476 + 0.7071067811865475im

julia> sqrt(1 + 2im)
1.272019649514069 + 0.7861513777574233im

julia> cos(1 + 2im)
2.0327230070196656 - 3.0518977991518im

julia> exp(1 + 2im)
-1.1312043837568135 + 2.4717266720048188im

julia> sinh(1 + 2im)
-0.4890562590412937 + 1.4031192506220405im
```

作用在实数上的数学函数，返回值一般为实数；作用在复数上的，返回值为复数。例如， sqrt 对 -1 和 -1 + 0im 的结果不同，即使 -1 == -1 + 0im ：

```julia
julia> sqrt(-1)
ERROR: DomainError
sqrt will only return a complex result if called with a complex argument.
try sqrt(complex(x))
 in sqrt at math.jl:131

julia> sqrt(-1 + 0im)
0.0 + 1.0im
```

补课用于使用变量构造复数，不许显示的写出乘号：

```julia
julia> a = 1; b = 2; a + b*im
1 + 2im
```

虽然可以，但不推荐使用函数`complex`构造复数：

```juli`
julia> a = 1; b = 2; complex(a, b)
1 + 2im
```

`Inf`和`NaN`也可以用于构造复数：

```julia
julia> 1 + Inf*im
1.0 + Inf*im

julia> 1 + NaN*im
1.0 + NaN*im
```

#### 有理数

Julia使用`//`表示分数：

```julia
julia> 2//3
2//3
```

如果分子、分母有公约数，将自动约简至最简分数，且分母为非负数：

```julia
julia> 6//9
2//3

julia> -4//8
-1//2

julia> 5//-15
-1//3

julia> -4//-12
1//3
```

`numerator`和`denominator`获取分数的分子与分母：

```julia
julia> numerator(2//3)
2

julia> denominator(2//3)
3
```

分子分母比较没啥必要，有比较运算和标准算术：

```julia
julia> 2//3 == 6//9
true

julia> 2//3 == 9//27
false

julia> 3//7 < 1//2
true

julia> 3//4 > 2//3
true

julia> 2//4 + 1//6
2//3

julia> 5//12 - 1//4
1//6

julia> 5//8 * 3//12
5//32

julia> 6//5 / 10//7
21//25
```

分数可以很简单的转化为浮点数：

```julia
julia> floag(3//4)
0.75
```

可以构造结果为`Inf`的分数：

```julia
julia> 5//0
1//0

julia> -3//0
-1//0

julia> typeof(ans)
Rational{Int64} (constructor with 1 method)
```

但是不可以构造结果为`NaN`的分数：

```julia
julia> 0//0
ERROR: invalid rational: 0//0
 in Rational at rational.jl:6
 in // at rational.jl:15
```

类型提升系统使得分数类型与其它数值类型交互非常简单：

```julia
julia> 3//5 + 1
8//5

julia> 3//5 - 0.5
0.09999999999999998

julia> 2//7 * (1 + 2im)
2//7 + 4//7*im

julia> 2//7 * (1.5 + 2im)
0.42857142857142855 + 0.5714285714285714im

julia> 3//2 / (1 + 2im)
3//10 - 3//5*im

julia> 1//2 + 2im
1//2 + 2//1*im

julia> 1 + 2//3im
1//1 - 2//3*im

julia> 0.5 == 1//2
true

julia> 0.33 == 1//3
false

julia> 0.33 < 1//3
true

julia> 1//3 - 0.33
0.0033333333333332993
```
