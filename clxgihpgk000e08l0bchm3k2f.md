---
title: "Coercion in JavaScript"
seoTitle: "JavaScript Type Coercion Explained"
seoDescription: "Understanding coercion in JavaScript: implicit and explicit type conversions, their scenarios, and methods to ensure predictable code behavior"
datePublished: Sat Jun 15 2024 19:29:41 GMT+0000 (Coordinated Universal Time)
cuid: clxgihpgk000e08l0bchm3k2f
slug: coercion-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1718479605121/243ad4d5-ade1-4c7d-bf03-073a8947d7d5.png
tags: js, javascript

---

Coercion is the conversion of one type into another either by explicitly calling the methods or by the language itself. There are two types of coercion in JavaScript

1. **Implicit Coercion**
    
2. **Explicit Coercion**
    

## Implicit Coercion

Implicit coercion in JavaScript refers to the automatic conversion of values from one type to another by the JavaScript engine. This can happen in various contexts, such as arithmetic operations, logical operations, and comparisons. While implicit coercion can make code more concise, it can also lead to unexpected behavior if not carefully managed.

#### Scenarios of Implicit Coercion

1. **Arithmetic Operations** JavaScript converts values to numbers when performing arithmetic operations.
    

```javascript
let result = "5" - 2;  // 3, string "5" is implicitly converted to number 5 
result = "5" * "2";    // 10, both strings are converted to numbers 
result = "5" / "2";    // 2.5, both strings are converted to numbers 
result = "5" + 2;      // "52", number 2 is converted to string "2"
```

2. **Logical Operations** Logical operations often trigger boolean coercion.
    

```javascript
let value = "hello" || 0;  // "hello", non-empty string is truthy 
value = "" && "world";     // "", empty string is falsy
```

3. **Comparisons** Equality (`==`) and inequality (`!=`) operators perform type coercion if the operands are of different types.
    

```javascript
let isEqual = "5" == 5;    // true, string "5" is converted to number 5 
isEqual = null == undefined;  // true, `null` and `undefined` are considered equal isEqual = "0" == false;    // true, string "0" is converted to number 0 and compared to false (which is also 0)
```

## Explicit Coercion

Explicit coercion in JavaScript refers to the conversion of a value from one data type to another. This is done using specific methods or operators provided by the language, rather than relying on the implicit type conversion that JavaScript sometimes performs automatically.

Explicit coercion is useful in many scenarios:

* **Form data**: When working with form inputs, you often need to convert string values to numbers or other types.
    
* **JSON handling**: When parsing JSON data, you may need to convert strings to appropriate data types.
    
* **API interactions**: When dealing with APIs, you might need to convert data types to match the expected input or output formats.
    

#### To String

1. **toString() method:** `toString()` method converts an object to a string. It can be called on numbers, boolean, arrays, and many other objects. However, for `null` and `undefined`, it will throw an error
    

```javascript
let num = 123;
let str = num.toString();  // "123"

let bool = true;
let strBool = bool.toString();  // "true"

let arr = [1, 2, 3];
let strArr = arr.toString();  // "1,2,3"
```

2. **String() Function:** The `String()` function converts various types of values into strings
    

```javascript
let num = 123;
let str = String(num);  // "123"

let bool = true;
let strBool = String(bool);  // "true"

let obj = {key: "value"};
let strObj = String(obj);  // "[object Object]"

let arr = [1, 2, 3];
let strArr = String(arr);  // "1,2,3"
```

In case of an array both returns a comma separated string notation of elements and for objects by default it logs `[object Object]` until a custom `toString()` function is implemented.

#### To Number

1. **Number() function:** Converts a value to a number
    

```javascript
let str = "123";
let num = Number(str);  // 123

let bool = true;
let numBool = Number(bool);  // 1

let emptyStr = "";
let numEmptyStr = Number(emptyStr);  // 0

let arr = [1, 2, 3];
let numArr = Number(arr);  // NaN (arrays are not converted to numbers this way)
```

2. **parseInt() function:** The `parseInt()` function parses a string argument and returns an integer of the specified radix (the base in mathematical numeral systems). It is tolerant of non-numeric characters. It stops parsing when encountering a non-numeric character. For non-string values, it first converts to a string equivalent and then parses the number.
    

```javascript
parseInt(string, radix);
```

* `string`: The value to parse. If this argument is not a string, it is converted to a string (using `String` abstract operation).
    
* `radix`: An integer between 2 and 36 that represents the radix (the base in mathematical numeral systems) of the string.
    

```javascript
let str = "123";
let num = parseInt(str, 10);  // 123

let hexStr = "0xFF";
let numHex = parseInt(hexStr, 16);  // 255

let binStr = "1010";
let numBin = parseInt(binStr, 2);  // 10
```

3. **parseFloat() function:** The `parseFloat()` function parses a string argument and returns a floating-point number.
    

```javascript
let str = "123.45";
let num = parseFloat(str);  // 123.45

let strInt = "123";
let numInt = parseFloat(strInt);  // 123

let strWithText = "123.45abc";
let numWithText = parseFloat(strWithText);  // 123.45
```

#### To Boolean

1. **Boolean() function:** Converts a value to boolean.
    

```javascript
let num = 0;
let bool = Boolean(num);  // false

let str = "hello";
let boolStr = Boolean(str);  // true

let emptyArr = [];
let boolArr = Boolean(emptyArr);  // true

let nullValue = null;
let boolNull = Boolean(nullValue);  // false
```

2. **Double Negation(**`!!`**):** Converts a value to boolean by first negating it twice.
    

```javascript
let num = 1;
let bool = !!num;  // true

let str = "";
let boolStr = !!str;  // false**

let obj = {};
let boolObj = !!obj;  // true

let undefinedValue;
let boolUndefined = !!undefinedValue;  // false**
```

\*\* In JavaScript, "falsy" values are values that, when evaluated in a boolean context, are considered `false`. This concept is critical for understanding control flow and conditions in JavaScript. The falsy values in JavaScript are:

1. `false`
    
2. `0` (zero)
    
3. `-0` (negative zero)
    
4. `0n` (BigInt zero)
    
5. `""` (empty string)
    
6. `null`
    
7. `undefined`
    
8. `NaN` (Not-a-Number)
    

> Implicit coercion can make code concise but can also introduce bugs if not understood properly. By using explicit coercion and being aware of the rules of implicit coercion, we can write more predictable and robust JavaScript code.