## Expressions

TODO()

### Constant literals

Constant literals are expressions that correspond to constant, non-changing values.
Every constant literal is defined to have a single standard library type, whichever
it is defined to be on current platform.

#### Boolean literals

**_BooleanLiteral_:**  
  ~  `true` | `false`

Keywords `true` and `false` denote boolean literals of corresponding values.
These are two strong keywords and as such cannot be used as identifiers unless [escaped][Escaped identifiers].
Values `true` and `false` always have type `kotlin.Bool`.

#### Integer literals

**_IntegerLiteral_:**  
  ~  _DecDigitNoZero_ {_DecDigitOrSeparator_} _DecDigit_
      | _DecDigit_

**_HexLiteral_:**  
  ~  `0` (`x`|`X`) _HexDigit_ {_HexDigitOrSeparator_} _HexDigit_   
      | `0` (`x`|`X`) _HexDigit_

**_BinLiteral_:**  
  ~  `0` (`b`|`B`) _BinDigit_ {_BinDigitOrSeparator_} _BinDigit_   
      | `0` (`b`|`B`) _BinDigit_

**_DecDigitNoZero_:**  
  ~  _DecDigit_ - `0`

**_DecDigitOrSeparator_:**  
  ~  _DecDigit_ | _Underscore_

**_HexDigitOrSeparator_:**  
  ~  _HexDigit_ | _Underscore_

**_BinDigitOrSeparator_:**  
  ~  _BinDigit_ | _Underscore_

**_DecDigits_:**  
  ~  _DecDigit_ {_DecDigitOrSeparator_} _DecDigit_ | _DecDigit_

##### Decimal integer literals

A sequence of decimal digit symbols (`0` though `9`) is a decimal integer literal.
Digits may be separated by the underscore symbol, but no underscore can be placed
before the first digit or after the last one. Please note that unlike other
languages Kotlin does not support octal literals. Even more, any decimal literal
starting with digit `0` and containing more than 1 digit is not a valid decimal literal.

Decimal literals may be suffixed by the long literal mark (`L` symbol).
A decimal literal with the mark has type `kotlin.Long`, while a literal without it
has type `kotlin.Int` if its value is below $2^{31}-1$ or type `kotlin.Long` otherwise.

##### Hexadecimal integer literals

A sequence of hexadecimal digit symbols (`0` through `9`, `a` through `f`, or `A` through `F`)
prefixed by `0x` or `0X` is a hexadecimal integer literal. Digits may be separated by the underscore symbol,
but no underscore can be placed before the first digit or after the last one.

Hexadecimal literals may be suffixed by the long literal mark (`L` symbol).
A hexadecimal literal with the mark has type `kotlin.Long`, while a literal without it
has type `kotlin.Int` if its value is below $2^{31}-1$ or type `kotlin.Long` otherwise.

##### Binary integer literals

A sequence of binary digit symbols (`0` or `1`)
prefixed by `0b` or `0B` is a binary integer literal. Digits may be separated by the underscore symbol,
but no underscore can be placed before the first digit or after the last one.

Binary literals may be suffixed by the long literal mark (`L` symbol).
A binary literal with the mark has type `kotlin.Long`, while a literal without it
has type `kotlin.Int` if its value is below $2^{31}-1$ or type `kotlin.Long` otherwise.

#### Real literals

**_RealLiteral_:**  
  ~  _FloatLiteral_ | _DoubleLiteral_

**_FloatLiteral_:**  
  ~  _DoubleLiteral_ (`f` | `F`)
      | _DecDigits_ (`f` | `F`)

**_DoubleLiteral_:**  
  ~  [_DecDigits_] `.` _DecDigits_ [_DoubleExponent_]
      | _DecDigits_ _DoubleExponent_

A *real literal* consists of the following parts: the whole-number part, a
decimal point (represented by the ASCII period character (`.`)), a fraction part
and an exponent. Unlike other languages, Kotlin real literals may only be expressed
in decimal numbers. The number also may be followed by type suffix (`f` or `F`).

The exponent is an exponent mark (`e` or `E`) followed by an optionaly signed
decimal integer (a sequence of decimal digits).

The whole-number part and the exponent part may be omitted. The fraction part may
only be omitted together with the decimal point if the whole part and either the
exponent part or type suffix are present. Unlike other languages, Kotlin does not
support omitting the fraction part, but leaving the decimal point in.

The digits of the whole-number part or the fraction part or the exponent may be optionally
separated by underscores, but an underscore may not be placed between, before, or after
these parts. It also may not be placed before or after the exponent sign symbol.

A real literal without a type suffix has type `kotlin.Double`, while a real literal
with the type suffix does have type `kotlin.Float`. There is no special suffix
attributed to the `kotlin.Double` type.

#### Character literals

**_CharacterLiteral_:**  
  ~  `'` (_EscapeSeq_ | _<any character except CR, LF, `'` and `\`>_) `'`

**_EscapeSeq_:**  
  ~  _UnicodeCharacterLiteral_ | _EscapedCharacter_

**_UnicodeCharacterLiteral_:**  
  ~  `\` `u` _HexDigit_ _HexDigit_ _HexDigit_ _HexDigit_

**_EscapedCharacter_:**  
  ~  `\` (`t` | `b` | `r` | `n` | `'` | `"` | `\` | `$`)

A **character literal** defines a constant holding a unicode character value.
A simply-formed character literal is any symbol between two single quotation mark
symbols (ASCII single quotation `'`), excluding newline symbols (*CR* and *LF*),
the single quotation symbol itself and the escaping mark (the ASCII backslash symbol `\`).

A character literal may also contain an escaped symbol of two kinds: a simple
escaped symbol or a unicode codepoint. Simple escaped symbols include:

- `\t` --- the unicode TAB symbol (TODO());
- `\b` --- the unicode BACKSPACE symbol(TODO());
- `\r` --- *CR*;
- `\n` --- *LF*;
- `\'` --- the unicode single quotation symbol(TODO());
- `\"` --- the unicode double quotation symbol(TODO());
- `\\` --- the unicode backslash symbol symbol(TODO());
- `\$` --- the unicode DOLLAR symbol.

A unicode codepoint escape sequence is the symbols `\u` followed by exactly four
hexadecimal digits. It represents the unicode symbol with the codepoint equal
to the number represented by these digits.
Please note that unicode escapes support only unicode symbols
in range U+0000 to U+FFFF.

Any character literal has type `kotlin.Char`.

#### String literals

Kotlin supports [string interpolation][String Interpolation] mechanisms
that supersede traditional string literals. Please refer to the corresponding
section.

#### Null literal

The keyword `null` signifies the **null reference**, which is a valid value for all
[nullable types][Nullable types].
Null reference implicitly has the nullable `kotlin.Nothing?` type and is, by definition,
the only valid value for this type (see [the corresponding section][`kotlin.Nothing`]).

TODO(): reshuffle these sections

### Conditional expression

**_ifExpression_:**  
  ~  `if` {_NL_} `(` {_NL_} _expression_ {_NL_} `)` {_NL_} _controlStructureBody_ [[`;`] {_NL_} `else` {_NL_} _controlStructureBody_]   
    | `if` {_NL_} `(` {_NL_} _expression_ {_NL_} `)` {_NL_} [`;` {_NL_}] `else` {_NL_} _controlStructureBody_   

**Conditional expressions** use the boolean value of one expression (*condition*) to decide
which of two other expressions (*branches*) should be evaluated.
If the condition evaluates to `true`, than the first branch (the true branch) is
evaluated, otherwise the second branch is.
The value of the resulting expression is the same as the value of the chosen branch.
The type of the resulting expression is
the [least upper bound][Least upper bound] of the types of two branches (TODO(): not that simple).
If one of the branches is omitted (see the grammar entry above), the resulting expression
has type [`kotlin.Unit`][`kotlin.Unit`] and the whole construct may not be used as an expression,
but only as a statement.

The condition expression must have type `kotlin.Boolean` (TODO(): or be smartcasted to it!),
otherwise it is a type error.

> When used as expressions, conditional expressions are special in the sense of operator
> precedence: they have the highest (same as all primary expressions) priority when
> placed on the right side of any binary expression, but when placed on the left side,
> they have the lowest priority. For details, see the [grammar][Syntax grammar]

### When expression

**_whenExpression_:**  
  ~  `when` {_NL_} [`(` _expression_ `)`] {_NL_} `{` {_NL_} {_whenEntry_ {_NL_}} {_NL_} `}`   

**_whenEntry_:**  
  ~  _whenCondition_ {{_NL_} `,` {_NL_} _whenCondition_} {_NL_} `->` {_NL_} _controlStructureBody_ [_semi_]   
    | `else` {_NL_} `->` {_NL_} _controlStructureBody_ [_semi_]   

**_whenCondition_:**  
  ~  _expression_   
    | _rangeTest_   
    | _typeTest_   

**_rangeTest_:**  
  ~  _inOperator_ {_NL_} _expression_   

**_typeTest_:**  
  ~  _isOperator_ {_NL_} _type_   

**When expression** is alike a **conditional expression** in the sense that it allows
several different other expressions (*cases*) to be evaluated depending on boolean conditions.
The key difference, however, is that when expressions may include several different
conditions. When expression has two different forms: with bound value and without it.

**When expression without bound value** (the form where the expression enclosed in parantheses is absent)
evaluates one of the many different expressions based on corresponding conditions present
in the same *when entry*. Each entry consists of a boolean *condition* (or a special `else` condition),
each of which is checked and evaluated in order of appearance. If the current condition
evaluates to `true`, the corresponding expression is evaluated and the value of
when expression is the same as the evaluated expression. All remaining conditions and expressions
are not evaluated. The `else` branch is a special branch that evaluates if none of
the branches above it evaluated to `true`.

> Informally speaking, you can always replace the `else` branch with literal `true` and
> the semantics of the entry would not change

The `else` entry is also special in the sense that it **must** be the last entry
in the expression, otherwise a compiler error must be generated.

**When expression with bound value** (the form where the expression enclosed in parantheses is present)
are very similar to the form without bound value, but use different syntax for conditions.
In fact, it supports three different condition forms:

- *Type test condition*: type checking operator [TODO: link] followed by type. The
  condition generated is a type check expression [TODO: link] with the same operator
  and the same type, but an implicit left hand side, which has the same value as the bound
  expression.
- *Contains test condition*: containment operator [TODO: link] followed by an expression; The
  condition generated is a containment check expression [TODO: link] with the same operator
  and the same right hand side expression, but an implicit left hand side, which has the same value as the bound
  expression.
- *Any other expression*. The condition generated is an equality operator [TODO: link], with
  the left hand side being the bound expression, and the right hand side being the expression placed inside
  the entry.
- The `else` condition, which works the exact same way as it would in the form
  without bound expression.

> This also means that if this form of `when` contains a boolean expression, it is not
> checked directly as if it would be in the other form, but rather checked for **equality**
> with the bound variable, which is not the same thing.

The type of the resulting expression is
the [least upper bound][Least upper bound] of the types of all the entries (TODO(): not that simple).
If the expression is not [exhaustive][Exhaustive when expressions], it
has type [`kotlin.Unit`][`kotlin.Unit`] and the whole construct may not be used as an expression,
but only as a statement.

#### Exhaustive when expressions

A when expression is called **_exhaustive_** if at least one of the following is true:

- It has an `else` entry;
- It has a bound value and at least one of the following holds:
    - The bound expression is of type `kotlin.Boolean` and the conditions contain
      both:
        - A [constant expression][Constant expressions] evaluating to value `true`;
        - A [constant expression][Constant expressions] evaluating to value `false`;
    - The bound expression is of a [`sealed class`][Sealed classes] type and all its possible subtypes
      are covered using type test conditions of this expression;
    - The bound expression is of an [`enum class`][Enum classes] type and all enumerated values
      are checked for equality using constant conditions.

### Logical disjunction expression

**_disjunction_:**  
  ~  _conjunction_ {{_NL_} `||` {_NL_} (_conjunction_ | _ifExpression_)}   

Operator symbol `||` performs logical disjunction over two values of type `kotlin.Boolean`.
Note that this operator is **lazy**, meaning that it does not evaluate the right hand side
argument unless the left hand side argument evaluated to `false`.

### Logical conjunction expression

**_conjunction_:**  
  ~  _equality_ {{_NL_} `&&` {_NL_} (_equality_ | _ifExpression_)}   

Operator symbol `&&` performs logical conjunction over two values of type `kotlin.Boolean`.
Note that this operator is **lazy**, meaning that it does not evaluate the right hand side
argument unless the left hand side argument evaluated to `true`.

### Equality expressions

**_equality_:**  
  ~  _comparison_ {_equalityOperator_ {_NL_} (_comparison_ | _ifExpression_)}   

**_equalityOperator_:**  
  ~  `!=`   
    | `!==`   
    | `==`   
    | `===`   

Equality expressions are binary expressions involving equality operators. There are
two kinds of equality operators: *reference equality operators* and
*value equality operators*.

#### Reference equality expressions

*Reference equality expressions* are binary expressions employing reference equality operators:
`===` and `!==`. These expressions check if two values are equal *by reference*, meaning
that two values are equal (non-equal for operator `!==`) if and only if they represent the
same runtime value created using the same constructor call.

For values created without
construction calls, notably the constant literals and constant expressions composed
of those literals, the following holds:

- If these values are [non-equal by value][Value equality expressions], they are also
  non-equal by reference;
- Any instance of the null reference `null` is reference-equals to any other
  instance of the null reference;
- Otherwise, it is implementation-defined and must not be used as a means of comparing
  two such values.

Reference equality expressions always have type `kotlin.Boolean`.

#### Value equality expressions

*Value equality expressions* are binary expressions employing value equality operators:
`==` and `!=`. These operators are [overloadable][Overloadable operators] with the following
expansion:

- $A$ `==` $B$ is exactly the same as $A$`?.equals(`$B$`) ?: (`$B$` === null)` where `equals` is a valid
  operator function available in the current scope;
- $A$ `!=` $B$ is exactly the same as `!(`$A$`?.equals(`$B$`) ?: (`$B$` === null))` where `equals` is a valid
  operator function available in the current scope.

> Please note that the class `kotlin.Any` has a built-in open operator member function called `equals`,
> meaning that there is always at least one available overloading candidate for any value equality expression.

Value equality expressions always have type `kotlin.Boolean`. If the corresponding operator function
has a different return type, it is invalid and a compiler error should be generated.

### Comparison expressions

**_comparison_:**  
  ~  _infixOperation_ [_comparisonOperator_ {_NL_} (_infixOperation_ | _ifExpression_)]   

**_comparisonOperator_:**  
  ~  `<`   
    | `>`   
    | `<=`   
    | `>=`   

*Comparison expressions* are binary expressions employing the comparison operators:
`<`, `>`, `<=` and `>=`. These operators are [overloadable][Overloadable operators] with the following
expansion:

- $A$`<`$B$ is exactly the same as $A$`.compareTo(`$B$`) [<] 0`
- $A$`>`$B$ is exactly the same as `0 [<] `$A$`.compareTo(`$B$`)`
- $A$`<=`$B$ is exactly the same as `!(`$A$`.compareTo(`$B$`) [<] 0)`
- $A$`>=`$B$ is exactly the same as `!(0 [<] `$A$`.compareTo(`$B$`))`

where `compareTo` is a valid operator function available in the current scope
and `[<]` (read "boxed less") is a special operator unavailable for in-code use in Kotlin and performing
integer "less-than" comparison of two integer numbers. The `compareTo` overloaded function
must have return type `kotlin.Int`, otherwise it's a compiler error.

All comparison expressions always have type `kotlin.Boolean`.

### Type-checking and containment-checking expressions

**_infixOperation_:**  
  ~  _elvisExpression_ {_inOperator_ {_NL_} (_elvisExpression_ | _ifExpression_) | _isOperator_ {_NL_} _type_}   

**_inOperator_:**  
  ~  `in` | `!in`   

**_isOperator_:**  
  ~  `is` | `!is`   

#### Type-checking expression

A type checking expression employs the use of an type-checking operators `is` or `!is`
and has an expression as a left-hand side operand and a type name as a right-hand
side operand. The type must be [runtime-available][Runtime-available types], otherwise
a compiler error should be generated. The expression checks whether the runtime type of
the expression on the left is the same (not the same for `!is`) as the type denoted
by the right-hand side argument.

Type-checking expression always has type `kotlin.Boolean`.

##### TODO()

- Smart casts!

#### Containment-checking expression

A *containment-checking expression* is a binary expression employing the containment operator
(`in` or `!in`). These are [overloadable][Overloadable operators] operators with the following expansion:

- $A$` in `$B$ is exactly the same as $B$`.contains(`$B$`)`;
- $A$` !in `$B$ is exactly the same as `!(`$B$`.contains(`$B$`))`;

where `contains` is a valid operator function available in the current scope. This
function must have return type `kotlin.Boolean`, otherwise a compiler error is generated.
Containment-checking expressions always have type `kotlin.Boolean`.

### Elvis operator expression

**_elvisExpression_:**  
  ~  _infixFunctionCall_ {{_NL_} `?:` {_NL_} (_infixFunctionCall_ | _ifExpression_)}   

*Elvis operator expression* is a binary expression that emplys the elvis operator (`?:`).
It checks whether the left-hand side expression is equal to `null`, and if it is,
evaluates and return the right-hand side expression.

This operator is **lazy**, meaning that if the left-hand side expression is not equal
to `null`, the right-hand side expression is never evaluated.

The type of elvis operator expression is the [least upper bound][The least upper bound]
of the non-nullable variant of the type of the left-hand side expression and the
type of the right-hand side expression. TODO(): not that simple, too

### Range expression

**_rangeExpression_:**  
  ~  _additiveExpression_ {`..` {_NL_} (_additiveExpression_ | _ifExpression_)}   

A *range expression* is a binary expression employing the range operator `..`.
It is an [overloadable][Overloadable operators] operator with the following expansion:

- $A$`..`$B$ is exactly the same as $A$`.rangeTo(`$B$`)`

where `rangeTo` is a valid operator function available in the current scope.
The return type of this function is not restricted.
The range expression has the same type as the return type of the corresponding
`rangeTo` overload variant.

### Additive expression

**_additiveExpression_:**  
  ~  _multiplicativeExpression_ {_additiveOperator_ {_NL_} (_multiplicativeExpression_ | _ifExpression_)}   

**_additiveOperator_:**  
  ~  `+` | `-`   

An *additive expression* is a binary expression employing the addition (`+`) or subtraction (`-`) operators.
These are [overloadable][Overloadable operators] operators with the following expansions:

- $A$`+`$B$ is exactly the same as $A$`.plus(`$B$`)`
- $A$`-`$B$ is exactly the same as $A$`.minus(`$B$`)`

where `plus` or `minus` is a valid operator function available in the current scope.
The return type of this function is not restricted.
The range expression has the same type as the return type of the corresponding
operator function overload variant.

### Multiplicative expression

**_multiplicativeExpression_:**  
  ~  _asExpression_ {_multiplicativeOperator_ {_NL_} (_asExpression_ | _ifExpression_)}   

**_multiplicativeOperator_:**  
  ~  `*`   
    | `/`   
    | `%`   

An *multiplicative expression* is a binary expression employing the multiplication (`*`), division (`/`) or remainder (`%`) operators.
These are [overloadable][Overloadable operators] operators with the following expansions:

- $A$`*`$B$ is exactly the same as $A$`.times(`$B$`)`
- $A$`/`$B$ is exactly the same as $A$`.div(`$B$`)`
- $A$`%`$B$ is exactly the same as $A$`.rem(`$B$`)` or $A$`.mod(`$B$`)`, whichever is available

> As of Kotlin version 1.2.30, the `mod` form of remainder operator is deprecated

where `times`, `div`, `rem` or `mod` is a valid operator function available in the current scope.
The return type of this function is not restricted.
The range expression has the same type as the return type of the corresponding
operator function overload variant.

### Cast expression

**_asExpression_:**  
  ~  _prefixUnaryExpression_ [{_NL_} _asOperator_ {_NL_} _type_]   

**_asOperator_:**  
  ~  `as`   
    | `as?`   
    | `:`   

A *cast expression* is a binary expression employing the cast operators (`as` or `as?`) and
receives an expression as the left-hand side operand and a type name as the right-hand side operand.
This operator perform a runtime check whether runtime type of the expression
is a [subtype][Subtyping] of the type given on the right-hand side operand and
throws an exception otherwise.

#### TODO()

- Smart casts!
- It doesn't really work that way if the type is not runtime-available
- `as?` returns null (or not, see above)



### Not-null assertion operator expression

### Operator expressions

### Safe call expression

### Type check expression

## TODOS()

- Control structure body typing
- Overloadable operators && operator expansion
- Smart casts vs compile-time types
- The whole "used as an expression" vs "used as a statement" business
