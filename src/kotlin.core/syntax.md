## Syntax

### Grammar

#### Lexical grammar

##### Character classes

**_LF_:**  
  ~  _<unicode character Line Feed U+000A>_

**_CR_:**  
  ~  _<unicode character Carriage Return U+000D>_

**_WS_:**  
  ~  _<one of the following characters: SPACE U+0020, TAB U+0009, Form Feed U+000C>_

**_Underscore_:**  
  ~  _<unicode character Low Line U+005F>_

**_Letter_:**  
  ~  _<any unicode character from classes Ll, Lm, Lo, Lt, Lu or Nl>_

**_UnicodeDigit_:**  
  ~  _<any unicode character from class Nd>_

**_LineCharacter_:**  
  ~  _<any unicode character excluding LF and CR>_

**_BinaryDigit_:**  
  ~  `0` | `1`

**_DecimalDigit_:**  
  ~  `0` | `1` | `2` | `3` | `4` | `5` | `6` | `7` | `8` | `9`

**_HexDigit_:**  
  ~  _DecimalDigit_   
      | `A` | `B` | `C` | `D` | `E` | `F`   
      | `a` | `b` | `c` | `d` | `e` | `f`

### Keywords and operators

**_Operator_:**  
  ~  `.` | `,` | `(` | `)` | `[` | `]` | `@[` | `{` | `}` | `*` | `%` | `/` | `+` | `-` | `++` | `--`   
      | `&&` | `||` | `!` | `!!` | `:` | `;` | `=` | `+=` | `-=` | `*=` | `/=` | `%=` | `->` | `=>`   
      | `..` | `::` | `?::` | `;;` | `#` | `@` | `?` | `?:` | `<` | `>` | `\m` | `>=` | `!=` | `!==`   
      | `==` | `===` | `'` | `"` | `"""`

**_SoftKeyword_:**  
  ~  `public` | `private` | `protected` | `internal`   
    | `enum` | `sealed` | `annotation` | `data` | `inner`   
    | `tailrec` | `operator` | `inline` | `infix` | `external`   
    | `suspend` | `override` | `abstract` | `final` | `open`   
    | `const` | `lateinit` | `vararg` | `noinline` | `crossinline`   
    | `reified` | `expect` | `actual`   

**_Keyword_:**  
  ~  `package` | `import` | `class` | `interface`   
    | `fun` | `object` | `val` | `var` | `typealias`   
    | `constructor` | `by` | `companion` | `init`   
    | `this` | `super` | `typeof` | `where`   
    | `if` | `else` | `when` | `try` | `catch`   
    | `finally` | `for` | `do` | `while` | `throw`   
    | `return` | `continue` | `break` | `as`   
    | `is` | `in` | `!is` | `!in` | `out`   
    | `get` | `set` | `dynamic` | `@file`   
    | `@field` | `@property` | `@get` | `@set`   
    | `@receiver` | `@param` | `@setparam` | `@delegate`   

##### Whitespace and comments

**_NL_:**  
  ~  _LF_ | _CR_ [_LF_]

**_ShebangLine_:**  
  ~  `#!` {_LineCharacter_}

**_LineComment_:**  
  ~  `//` {_LineCharacter_}

**_DelimitedComment_:**  
  ~  `/*` {_DelimitedComment_ | <any character>} `*/`

##### Number literals

**_RealLiteral_:**  
  ~  _FloatLiteral_ | _DoubleLiteral_

**_FloatLiteral_:**  
  ~  _DoubleLiteral_ (`f` | `F`)
      | _DecDigits_ (`f` | `F`)

**_DoubleLiteral_:**  
  ~  [_DecDigits_] `.` _DecDigits_ [_DoubleExponent_]
      | _DecDigits_ _DoubleExponent_

**_LongLiteral_:**  
  ~  (_IntegerLiteral_ | _HexLiteral_ | _BinLiteral_) `L`

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

**_BooleanLiteral_:**  
  ~  `true` | `false`

**_NullLiteral_:**  
  ~  `null`

##### Identifiers

**_Identifier_:**  
  ~  (_Letter_ | _Underscore_) {_Letter_ | _Underscore_ | _UnicodeDigit_}   
      | `` ` `` {_EscapedIdentifierCharacter_} `` ` ``

**_EscapedIdentifierCharacter_:**  
  ~  _<any character except CR, LF, `` ` ``, `[`, `]`, `<` or `>`>_

**_IdentifierOrSoftKey_:**  
  ~  _Identifier_ | _SoftKeyword_

**_AtIdentifier_:**  
  ~  `@` _IdentifierOrSoftKey_

**_IdentifierAt_:**  
  ~  _IdentifierOrSoftKey_ `@`

##### String literals

Syntax literals are fully defined in syntax grammar due to the complex nature of string interpolation

**_CharacterLiteral_:**  
  ~  `'` (_EscapeSeq_ | _<any character except CR, LF, `'` and `\`>_) `'`

**_EscapeSeq_:**  
  ~  _UnicodeCharacterLiteral_ | _EscapedCharacter_

**_UnicodeCharacterLiteral_:**  
  ~  `\` `u` _HexDigit_ _HexDigit_ _HexDigit_ _HexDigit_

**_EscapedCharacter_:**  
  ~  `\` (`t` | `b` | `r` | `n` | `'` | `"` | `\` | `$`)

**_FieldIdentifier_:**  
  ~  `$` _IdentifierOrSoftKey_

**_LineStrRef_:**  
  ~  _FieldIdentifier_

**_LineStrEscapedChar_:**  
  ~  _EscapedCharacter_ | _UnicodeCharacterLiteral_

**_LineStrExprStart_:**  
  ~  `${`

**_MultiLineStringQuote_:**  
  ~  `"` {`"`}

**_MultiLineStrRef_:**  
  ~  _FieldIdentifier_

**_MultiLineStrText_:**  
  ~  {<any character except `"` and `$`} | `$`

**_MultiLineStrExprStart_:**  
  ~  `${`

#### Syntax grammar

**_kotlinFile_:**  
  ~  [_shebangLine_] {_NL_} {_fileAnnotation_} _packageHeader_ _importList_ {_topLevelObject_} _EOF_   

**_script_:**  
  ~  [_shebangLine_] {_NL_} {_fileAnnotation_} _packageHeader_ _importList_ {statement _semi_} _EOF_   

**_fileAnnotation_:**  
  ~  `@file` `:` (`[` _unescapedAnnotation_+ `]` | _unescapedAnnotation_) _semi_   

**_packageHeader_:**  
  ~  [`package` _identifier_ _semi_]   

**_importList_:**  
  ~  {_importHeader_}   

**_importHeader_:**  
  ~  `import` _identifier_ [`.` `*` | _importAlias_] _semi_   

**_importAlias_:**  
  ~  `as` _simpleIdentifier_   

**_topLevelObject_:**  
  ~  _declaration_ _semis_   

**_classDeclaration_:**  
  ~  [_modifierList_] (`class` | `interface`) {_NL_} _simpleIdentifier_   
      [{_NL_} _typeParameters_] [{_NL_} _primaryConstructor_]   
      [{_NL_} `:` {_NL_} _delegationSpecifiers_]   
      [{_NL_} _typeConstraints_]   
      [{_NL_} _classBody_ | {_NL_} _enumClassBody_]   

**_primaryConstructor_:**  
  ~  [_modifierList_] [`constructor` {_NL_}] _classParameters_   

**_classParameters_:**  
  ~  `(` {_NL_} [_classParameter_ {{_NL_} `,` {_NL_} _classParameter_}] {_NL_} `)`   

**_classParameter_:**  
  ~  [_modifierList_] [`val` | `var`] {_NL_} _simpleIdentifier_ `:` {_NL_} _type_ [{_NL_} `=` {_NL_} _expression_]   

**_delegationSpecifiers_:**  
  ~  _annotatedDelegationSpecifier_ {{_NL_} `,` {_NL_} _annotatedDelegationSpecifier_}   

**_annotatedDelegationSpecifier_:**  
  ~  {_annotation_} {_NL_} _delegationSpecifier_   

**_delegationSpecifier_:**  
  ~  _constructorInvocation_   
    | _userType_   
    | _functionType_   
    | _explicitDelegation_   

**_constructorInvocation_:**  
  ~  _userType_ _callSuffix_   

**_explicitDelegation_:**  
  ~  (_userType_ | _functionType_) {_NL_} `by` {_NL_} _expression_   

**_classBody_:**  
  ~  `{` {_NL_} [_classMemberDeclarations_] {_NL_} `}`   

**_classMemberDeclarations_:**  
  ~  {_classMemberDeclaration_ _semis_} _classMemberDeclaration_ [_semis_]   

**_classMemberDeclaration_:**  
  ~  _declaration_   
    | _companionObject_   
    | _anonymousInitializer_   
    | _secondaryConstructor_   

**_anonymousInitializer_:**  
  ~  `init` {_NL_} _block_   

**_secondaryConstructor_:**  
  ~  [_modifierList_] `constructor` {_NL_} _functionValueParameters_ [{_NL_} `:` {_NL_} _constructorDelegationCall_] {_NL_} [_block_]   

**_constructorDelegationCall_:**  
  ~  `this` {_NL_} _valueArguments_   
    | `super` {_NL_} _valueArguments_   

**_enumClassBody_:**  
  ~  `{` {_NL_} [_enumEntries_] [{_NL_} `;` {_NL_} [_classMemberDeclarations_]] {_NL_} `}`   

**_enumEntries_:**  
  ~  _enumEntry_ {{_NL_} `,` {_NL_} _enumEntry_} {_NL_} [`,`]   

**_enumEntry_:**  
  ~  [modifierList {_NL_}] _simpleIdentifier_ [{_NL_} _valueArguments_] [{_NL_} _classBody_]   

**_functionDeclaration_:**  
  ~  [_modifierList_]   
    `fun`   
    [{_NL_} _typeParameters_]   
    [{_NL_} _type_ {_NL_} `.`]
    ({_NL_} _simpleIdentifier_)   
    {_NL_} _functionValueParameters_   
    [{_NL_} `:` {_NL_} _type_]   
    [{_NL_} _typeConstraints_]   
    [{_NL_} _functionBody_]   

**_functionValueParameters_:**  
  ~  `(` {_NL_} [_functionValueParameter_ {{_NL_} `,` {_NL_} _functionValueParameter_}] {_NL_} `)`   

**_functionValueParameter_:**  
  ~  [_modifierList_] _parameter_ [{_NL_} `=` {_NL_} _expression_]   

**_parameter_:**  
  ~  _simpleIdentifier_ {_NL_} [`:` {_NL_} _type_]   

**_functionBody_:**  
  ~  _block_   
    | `=` {_NL_} _expression_   

**_objectDeclaration_:**  
  ~  [_modifierList_] `object`   
      {_NL_} _simpleIdentifier_   
      [{_NL_} `:` {_NL_} _delegationSpecifiers_]   
      [{_NL_} _classBody_]   

**_companionObject_:**  
  ~  [_modifierList_] `companion` {_NL_} `object`   
      [{_NL_} _simpleIdentifier_]   
      [{_NL_} `:` {_NL_} _delegationSpecifiers_]   
      [{_NL_} _classBody_]   

**_propertyDeclaration_:**  
  ~  [_modifierList_] (`val` | `var`)   
      [{_NL_} _typeParameters_]   
      [{_NL_} _type_ {_NL_} `.`]   
      ({_NL_} (_multiVariableDeclaration_ | _variableDeclaration_))   
      [{_NL_} _typeConstraints_]   
      [{_NL_} (`by` | `=`) {_NL_} _expression_]   
      [NL+ `;`] {_NL_} [[_getter_] ({_NL_} [_semi_] _setter_] | [_setter_] [{_NL_} [_semi_] _getter_])   

**_multiVariableDeclaration_:**  
  ~  `(` {_NL_} _variableDeclaration_ {{_NL_} `,` {_NL_} _variableDeclaration_} {_NL_} `)`   

**_variableDeclaration_:**  
  ~  {_annotation_} {_NL_} _simpleIdentifier_ [{_NL_} `:` {_NL_} _type_]   

**_getter_:**  
  ~  [_modifierList_] `get`   
    | [_modifierList_] `get` {_NL_} `(` {_NL_} `)` [{_NL_} `:` {_NL_} _type_] {_NL_} _functionBody_   

**_setter_:**  
  ~  [_modifierList_] `set`   
    | [_modifierList_] `set` {_NL_} `(` {annotation | _parameterModifier_} _parameter_ `)` [{_NL_} `:` {_NL_} _type_] {_NL_} _functionBody_   

**_typeAlias_:**  
  ~  [_modifierList_] `typealias` {_NL_} _simpleIdentifier_ [{_NL_} _typeParameters_] {_NL_} `=` {_NL_} _type_   

**_typeParameters_:**  
  ~  `<` {_NL_} _typeParameter_ {{_NL_} `,` {_NL_} _typeParameter_} {_NL_} `>`   

**_typeParameter_:**  
  ~  [_modifierList_] {_NL_} _simpleIdentifier_ [{_NL_} `:` {_NL_} _type_]   

**_type_:**  
  ~  [_typeModifierList_]   
    ( _parenthesizedType_   
    | _nullableType_   
    | _typeReference_   
    | _functionType_)   

**_typeModifierList_:**  
  ~  (_annotation_ | `suspend` {_NL_} {_annotation_ | `suspend` {_NL_}})   

**_parenthesizedType_:**  
  ~  `(` _type_ `)`   

**_nullableType_:**  
  ~  (_typeReference_ | _parenthesizedType_) {_NL_} `?`+   

**_typeReference_:**  
  ~  `(` _typeReference_ `)`   
    | _userType_   
    | `dynamic`

**_functionType_:**  
  ~  [_receiverType_ {_NL_} `.` {_NL_}] _functionTypeParameters_  {_NL_} `\->` [{_NL_} _type_]   

**_receiverType_:**  
  ~  _parenthesizedType_   
    | _nullableType_   
    | _typeReference_   

**_userType_:**  
  ~  _simpleUserType_ {{_NL_} `.` {_NL_} _simpleUserType_}   

**_simpleUserType_:**  
  ~  _simpleIdentifier_ [{_NL_} _typeArguments_]   

**_functionTypeParameters_:**  
  ~  `[` {_NL_} (_parameter_ | _type_) {{_NL_} `,` {_NL_} (_parameter_ | _type_)} {_NL_} `)`   

**_typeConstraints_:**  
  ~  `where` {_NL_} _typeConstraint_ {{_NL_} `,` {_NL_} _typeConstraint_}   

**_typeConstraint_:**  
  ~  {_annotation_} _simpleIdentifier_ {_NL_} `:` {_NL_} _type_   

**_block_:**  
  ~  `{` {_NL_} _statements_ {_NL_} `}`   

**_statements_:**  
  ~  [_statement_ {semis _statement_} [_semis_]]   

**_statement_:**  
  ~  {_labelDefinition_}   
    ( _declaration_   
    | _assignment_   
    | _loopStatement_   
    | _expression_)   

**_declaration_:**  
  ~  _classDeclaration_   
    | _objectDeclaration_   
    | _functionDeclaration_   
    | _propertyDeclaration_   
    | _typeAlias_   

**_assignment_:**  
  ~  _directlyAssignableExpression_ `=` {_NL_} _expression_   
    | _assignableExpression_ _assignmentAndOperator_ {_NL_} _expression_   

**_expression_:**  
  ~  _disjunction_ | _ifExpression_   

**_ifExpression_:**  
  ~  `if` {_NL_} `(` {_NL_} _expression_ {_NL_} `)` {_NL_} _controlStructureBody_ [[`;`] {_NL_} `else` {_NL_} _controlStructureBody_]   
    | `if` {_NL_} `(` {_NL_} _expression_ {_NL_} `)` {_NL_} [`;` {_NL_}] `else` {_NL_} _controlStructureBody_   

**_disjunction_:**  
  ~  _conjunction_ {{_NL_} `||` {_NL_} (_conjunction_ | _ifExpression_)}   

**_conjunction_:**  
  ~  _equality_ {{_NL_} `&&` {_NL_} (_equality_ | _ifExpression_)}   

**_equality_:**  
  ~  _comparison_ {_equalityOperator_ {_NL_} (_comparison_ | _ifExpression_)}   

**_comparison_:**  
  ~  _infixOperation_ [_comparisonOperator_ {_NL_} (_infixOperation_ | _ifExpression_)]   

**_infixOperation_:**  
  ~  _elvisExpression_ {_inOperator_ {_NL_} (_elvisExpression_ | _ifExpression_) | _isOperator_ {_NL_} _type_}   

**_elvisExpression_:**  
  ~  _infixFunctionCall_ {{_NL_} `?:` {_NL_} (_infixFunctionCall_ | _ifExpression_)}   

**_infixFunctionCall_:**  
  ~  _rangeExpression_ {_simpleIdentifier_ {_NL_} (_rangeExpression_ | _ifExpression_)}   

**_rangeExpression_:**  
  ~  _additiveExpression_ {`..` {_NL_} (_additiveExpression_ | _ifExpression_)}   

**_additiveExpression_:**  
  ~  _multiplicativeExpression_ {_additiveOperator_ {_NL_} (_multiplicativeExpression_ | _ifExpression_)}   

**_multiplicativeExpression_:**  
  ~  _asExpression_ {_multiplicativeOperator_ {_NL_} (_asExpression_ | _ifExpression_)}   

**_asExpression_:**  
  ~  _prefixUnaryExpression_ [{_NL_} _asOperator_ {_NL_} _type_]   

**_prefixUnaryExpression_:**  
  ~  {_unaryPrefix_} _postfixUnaryExpression_   
    | _unaryPrefix_ {_unaryPrefix_} _ifExpression_   

**_unaryPrefix_:**  
  ~  _annotation_   
    | _labelDefinition_   
    | _prefixUnaryOperator_ {_NL_}   

**_postfixUnaryExpression_:**  
  ~  _primaryExpression_ {_postfixUnarySuffix_}   

**_postfixUnarySuffix_:**  
  ~  _postfixUnaryOperator_   
    | _typeArguments_   
    | _callSuffix_   
    | _indexingSuffix_   
    | _navigationSuffix_   

**_directlyAssignableExpression_:**  
  ~  _postfixUnaryExpression_ _assignableSuffix_   
    | _simpleIdentifier_   

**_assignableExpression_:**  
  ~  _prefixUnaryExpression_   

**_assignableSuffix_:**  
  ~  _typeArguments_   
    | _indexingSuffix_   
    | _navigationSuffix_   

**_indexingSuffix_:**  
  ~  `[` {_NL_} _expression_ {{_NL_} `,` {_NL_} _expression_} {_NL_} `]`   

**_navigationSuffix_:**  
  ~  {_NL_} _memberAccessOperator_ {_NL_} (_simpleIdentifier_ | `class`)   

**_callSuffix_:**  
  ~  [_typeArguments_] [_valueArguments_] _annotatedLambda_   
    | [_typeArguments_] _valueArguments_   

**_annotatedLambda_:**  
  ~  {annotation | _IdentifierAt_} {_NL_} _lambdaLiteral_   

**_valueArguments_:**  
  ~  `(` {_NL_} [_valueArgument_] {_NL_} `)`   
    | `(` {_NL_} _valueArgument_ {{_NL_} `,` {_NL_} _valueArgument_} {_NL_} `)`   

**_typeArguments_:**  
  ~  `<` {_NL_} _typeProjection_ {{_NL_} `,` {_NL_} _typeProjection_} {_NL_} `>`   

**_typeProjection_:**  
  ~  [_typeProjectionModifierList_] _type_ | `*`   

**_typeProjectionModifierList_:**  
  ~  {_varianceAnnotation_}   

**_valueArgument_:**  
  ~  [_annotation_] {_NL_} [_simpleIdentifier_ {_NL_} `=` {_NL_}] {`*`} {_NL_} _expression_   

**_primaryExpression_:**  
  ~  _parenthesizedExpression_   
    | _literalConstant_   
    | _stringLiteral_   
    | _simpleIdentifier_   
    | _callableReference_   
    | _functionLiteral_   
    | _objectLiteral_   
    | _collectionLiteral_   
    | _thisExpression_   
    | _superExpression_   
    | _whenExpression_   
    | _tryExpression_   
    | _jumpExpression_   

**_parenthesizedExpression_:**  
  ~  `(` {_NL_} _expression_ {_NL_} `)`   

**_collectionLiteral_:**  
  ~  `[` {_NL_} _expression_ {{_NL_} `,` {_NL_} _expression_} {_NL_} `]`   
    | `[` {_NL_} `]`   

**_literalConstant_:**  
  ~  _BooleanLiteral_   
    | _IntegerLiteral_   
    | _HexLiteral_   
    | _BinLiteral_   
    | _CharacterLiteral_   
    | _RealLiteral_   
    | _NullLiteral_   
    | _LongLiteral_   

**_stringLiteral_:**  
  ~  _lineStringLiteral_   
    | _multiLineStringLiteral_   

**_lineStringLiteral_:**  
  ~  `"` {_lineStringContent_ | _lineStringExpression_} `"`   

**_multiLineStringLiteral_:**  
  ~  `"""` {_multiLineStringContent_ | _multiLineStringExpression_ | _MultiLineStringQuote_} `"""`   

**_lineStringContent_:**  
  ~  _LineStrText_   
    | _LineStrEscapedChar_   
    | _LineStrRef_   

**_lineStringExpression_:**  
  ~  _LineStrExprStart_ _expression_ `}`   

**_multiLineStringContent_:**  
  ~  _MultiLineStrText_   
    | _MultiLineStringQuote_   
    | _MultiLineStrRef_   

**_multiLineStringExpression_:**  
  ~  _MultiLineStrExprStart_ {_NL_} _expression_ {_NL_} `}`   

**_lambdaLiteral_:**  
  ~  `{` {_NL_} _statements_ {_NL_} `}`   
    | `{` {_NL_} _lambdaParameters_ {_NL_} _ARROW_ {_NL_} _statements_ {_NL_} `}`   

**_lambdaParameters_:**  
  ~  [_lambdaParameter_] {{_NL_} `,` {_NL_} _lambdaParameter_}   

**_lambdaParameter_:**  
  ~  _variableDeclaration_   
    | _multiVariableDeclaration_ [{_NL_} `:` {_NL_} _type_]   

**_anonymousFunction_:**  
  ~  `fun`   
    [{_NL_} _type_ {_NL_} `.`]   
    {_NL_} _functionValueParameters_   
    [{_NL_} `:` {_NL_} _type_]   
    [{_NL_} _typeConstraints_]   
    [{_NL_} _functionBody_]   

**_functionLiteral_:**  
  ~  _lambdaLiteral_   
    | _anonymousFunction_   

**_objectLiteral_:**  
  ~  `object` {_NL_} `:` {_NL_} _delegationSpecifiers_ [{_NL_} _classBody_]   
    | `object` {_NL_} _classBody_   

**_thisExpression_:**  
  ~  `this` [_AtIdentifier_]

**_superExpression_:**  
  ~  `super` [`<` {_NL_} _type_ {_NL_} `>`] [_AtIdentifier_]

**_controlStructureBody_:**  
  ~  _block_   
    | _statement_   

**_whenExpression_:**  
  ~  `when` {_NL_} [`(` _expression_ `)`] {_NL_} `{` {_NL_} {_whenEntry_ {_NL_}} {_NL_} `}`   

**_whenEntry_:**  
  ~  _whenCondition_ {{_NL_} `,` {_NL_} _whenCondition_} {_NL_} `\->` {_NL_} _controlStructureBody_ [_semi_]   
    | `else` {_NL_} `\->` {_NL_} _controlStructureBody_ [_semi_]   

**_whenCondition_:**  
  ~  _expression_   
    | _rangeTest_   
    | _typeTest_   

**_rangeTest_:**  
  ~  _inOperator_ {_NL_} _expression_   

**_typeTest_:**  
  ~  _isOperator_ {_NL_} _type_   

**_tryExpression_:**  
  ~  `try` {_NL_} _block_ {{_NL_} _catchBlock_} [{_NL_} _finallyBlock_]   

**_catchBlock_:**  
  ~  `catch` {_NL_} `(` {_annotation_} _simpleIdentifier_ `:` _userType_ `)` {_NL_} _block_   

**_finallyBlock_:**  
  ~  `finally` {_NL_} _block_   

**_loopStatement_:**  
  ~  _forStatement_   
    | _whileStatement_   
    | _doWhileStatement_   

**_forStatement_:**  
  ~  `for` {_NL_} `(` {_annotation_} (variableDeclaration | _multiVariableDeclaration_) `in` _expression_ `)` {_NL_} [_controlStructureBody_]   

**_whileStatement_:**  
  ~  `while` {_NL_} `(` _expression_ `)` {_NL_} _controlStructureBody_   
    | `while` {_NL_} `(` _expression_ `)` {_NL_} `;`   

**_doWhileStatement_:**  
  ~  `do` {_NL_} [_controlStructureBody_] {_NL_} `while` {_NL_} `(` _expression_ `)`   

**_jumpExpression_:**  
  ~  `throw` {_NL_} _expression_   
    | (`return` | _RETURN_AT_) [_expression_]   
    | `continue` | _CONTINUE_AT_   
    | `break` | _BREAK_AT_   

**_callableReference_:**  
  ~  [_receiverType_] {_NL_} (`::`|`?::`) {_NL_} (_simpleIdentifier_ | `class`)   

**_assignmentAndOperator_:**  
  ~  `=`   
    | `+=`   
    | `-=`   
    | `*=`   
    | `/=`   
    | `%=`   

**_equalityOperator_:**  
  ~  `!=`   
    | `!==`   
    | `==`   
    | `===`   

**_comparisonOperator_:**  
  ~  `<`   
    | `>`   
    | `\<=`   
    | `>=`   

**_inOperator_:**  
  ~  `in` | `!in`   

**_isOperator_:**  
  ~  `is` | `!is`   

**_additiveOperator_:**  
  ~  `+` | `-`   

**_multiplicativeOperator_:**  
  ~  `*`   
    | `/`   
    | `%`   

**_asOperator_:**  
  ~  `as`   
    | `as?`   
    | `:`   

**_prefixUnaryOperator_:**  
  ~  `++`   
    | `--`   
    | `-`   
    | `+`   
    | `!`   

**_postfixUnaryOperator_:**  
  ~  `++`   
    | `--`   
    | `!!`   

**_memberAccessOperator_:**  
  ~  `.` | `?.` | `::`   

**_modifierList_:**  
  ~  (_annotation_ | _modifier_) {_annotation_ | _modifier_}   

**_modifier_:**  
  ~  (_classModifier_   
    | _memberModifier_   
    | _visibilityModifier_   
    | _varianceAnnotation_   
    | _functionModifier_   
    | _propertyModifier_   
    | _inheritanceModifier_   
    | _parameterModifier_   
    | _typeParameterModifier_   
    | _platformModifier_) {_NL_}   

**_classModifier_:**  
  ~  `enum`   
    | `sealed`   
    | `annotation`   
    | `data`   
    | `inner`   

**_memberModifier_:**  
  ~  `override`   
    | `lateinit`   

**_visibilityModifier_:**  
  ~  `public`   
    | `private`   
    | `internal`   
    | `protected`   

**_varianceAnnotation_:**  
  ~  `in`   
    | `out`   

**_functionModifier_:**  
  ~  `tailrec`   
    | `operator`   
    | `infix`   
    | `inline`   
    | `external`   
    | `suspend`   

**_propertyModifier_:**  
  ~  `const`   

**_inheritanceModifier_:**  
  ~  `abstract`   
    | `final`   
    | `open`   

**_parameterModifier_:**  
  ~  `vararg`   
    | `noinline`   
    | `crossinline`   

**_typeParameterModifier_:**  
  ~  `reified`   

**_platformModifier_:**  
  ~  `expect`   
    | `actual`   

**_labelDefinition_:**  
  ~  _IdentifierAt_ {_NL_}   

**_annotation_:**  
  ~  (singleAnnotation | _multiAnnotation_) {_NL_}   

**_singleAnnotation_:**  
  ~  _annotationUseSiteTarget_ `:` {_NL_} _unescapedAnnotation_   
    | _AtIdentifier_ {{_NL_} `.` _simpleIdentifier_} [_typeArguments_] [_valueArguments_]   

**_multiAnnotation_:**  
  ~  _annotationUseSiteTarget_ `:` `[` _unescapedAnnotation_ {_unescapedAnnotation_} `]`   
    | `@[` _unescapedAnnotation_+ `]`   

**_annotationUseSiteTarget_:**  
  ~  `@field`   
    | `@file`   
    | `@property`   
    | `@get`   
    | `@set`   
    | `@receiver`   
    | `@param`   
    | `@setparam`   
    | `@delegate`   

**_unescapedAnnotation_:**  
  ~  _identifier_ [_typeArguments_] [_valueArguments_]   

**_simpleIdentifier_:**  
  ~  _IdentifierOrSoftKey_

**_identifier_:**  
  ~  _simpleIdentifier_ {{_NL_} `.` _simpleIdentifier_}   

**_shebangLine_:**  
  ~  _ShebangLine_   

**_semi_:**  
  ~  (`;` | _NL_) {_NL_}   
    | _EOF_

**_semis_:**  
  ~  (`;` | _NL_) {`;` | _NL_}   
    | _EOF_
