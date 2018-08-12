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
