## Type system

### Glossary

`T`:: Type
`T!!`:: Non-nullable type
`T?`:: Nullable type
`{T!!}`:: Universe of non-nullable types
`{T?}`:: Universe of nullable types
$\langle T\rangle$:: Value of type $T$

### Introduction

Kotlin has a type system with the following main properties:

* static type checking
* null safety
* no unsafe implicit conversions
* unified root type
* nominal subtyping with bounded parametric polymorphism

TODO(static type checking)

Null safety is enforced by having two type universes --- _nullable_ (with nullable types `T?`) and _non-nullable_ (with non-nullable types `T!!`). All operations footnote:[Except for TODO()] which are allowed on nullable types are safe, i.e., should never cause a runtime null pointer error.

Implicit conversions between types in Kotlin are limited to safe upcasts w.r.t. subtyping, meaning all other (unsafe) conversions must be explicit, done via either a conversion function or an [explicit cast][Cast expression]. However, Kotlin also supports smart casts --- a special kind of implicit conversions which are safe w.r.t. program control- and data-flow, which are covered in more detail [here][Smart casts].

The unified supertype type for all types in Kotlin is `kotlin.Any?`, a nullable version of <<kotlin.Any>>.

Kotlin uses nominal subtyping, meaning subtyping relation is defined when a type is declared, with bounded parametric polymorphism, implemented as [generics][Generics].

### Built-in types

Kotlin type system uses the following built-in types, which have special semantics and representation (or lack thereof).

#### `kotlin.Any`

`kotlin.Any` is the unified supertype ($\top$) for `{T!!}`, i.e., all types are subtypes of `kotlin.Any`, either explicitly, implicitly, or by transitivity of subtyping relation.

#### `kotlin.Nothing`

`kotlin.Nothing` is the unified subtype ($\bot$) for `{T!!}`, i.e., `kotlin.Nothing` is a subtype of all non-nullable types, including user-defined ones. This makes it an uninhabited type (as it is impossible for anything to be a function and an integer at the same time), meaning instances of this type can never exist at runtime; subsequently, there is no way to create an instance of `kotlin.Nothing` in Kotlin.

As the evaluation of an expression with `kotlin.Nothing` type can never complete normally, it is used to mark special situations, such as:

* non-terminating expressions
* exceptional control flow
* control flow transfer

#### `kotlin.Unit`

`kotlin.Unit` is a unit type, i.e., a type with only one value `kotlin.Unit`; all values of type `kotlin.Unit` should reference the same underlying `kotlin.Unit` object.

TODO(Compare to `void`)

### Nullability

Kotlin supports null safety by having two kinds of types --- nullable and non-nullable. All type declarations, built-in or user-defined, create non-nullable types, i.e., types which cannot hold `null` value at runtime. To specify a nullable version of type `Foo`, one needs to use `Foo?` as a type.

NOTE: Informally, question mark means "type `T?` may hold values of type T or value `null`"

As arbitrary operations on `T?` may violate null safety, one has three options when working with nullable types:

1. Use safe operations
    * [safe call][Safe call expression]
2. Downcast from `T?` to `T!!`
    * [unsafe cast][Cast expression]
    * [type check][Type check expression] combined with [smart casts][Smart casts]
3. Supply a default value to use instead of `null`
    * [elvis operator][Elvis operator expression]

### Flexible types

### Platform types

### Subtyping

$<:$

### Generics

TODO(Here be a lot of dragons)
