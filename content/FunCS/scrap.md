---
draft: true
---

> [!abstract] Types
>> [!note] Types
>> A type is a defining shape of data, it describes a set of valid values which follow a set of restrictions.
>
>> [!example] Examples
>> - A ***Boolean*** is a logical *true/false* value. A Boolean can be either *true* or *false*.
>> - An ***Int*** is a whole *number* between -2,147,483,648 and 2,147,483,647
>> - A ***Char*** is a *unicode character*, representing symbols commonly found in text.
>> - A ***String*** is an *ordered*, *immutable* collection of *Chars
>> 
>

>[!abstract] Character Operations
>
>>[!definition] Character Addition
>>
>>$Add: (char, int) \rightarrow int$ returns the numeric result of adding a character's code and an integer
>>
>
>>[!property] Properties
>>
>>- Result is always an integer
>>- Original character is unchanged
>>- Common to cast result back to char
>
>>[!example]
>>```csharp
>>'A' + 1        // 66 (numeric value)
>>(char)('A' + 1) // 'B' (character value)
>>'Z' - 'A'      // 25 (positions between letters)
>>```
>

>[!abstract] Strings 🧶
>>[!Definition] 
>>
>>A *String* is an indexed immutable collection of characters.
>
>>[!property] Properties
>>
>>- Fixed length once created
>>- Zero-based indexing
>>- Always uses double quotes
>
>>[!example]
>>```csharp
>>"Alice";  // the string literal for the name "Alice"
>>"Alice"[0];    // evaluates to 'A'
>>"Alice"[4];     // evaluates to 'e'
>>```
>

>[!abstract] Integer Division
>
>>[!definition] Integer Division
>>
>> $Divide: (int, int) \rightarrow int$ returns the quotient of two integers, discarding any remainder.
>
>>[!property] Properties of Integer Division
>> - **Division by Zero:** Division by zero results in a `DivideByZeroException`.
>> - **Truncation:** The result is always an integer. The fractional part of the division is discarded. For example, `7 / 3` results in `2`, not `2.333...`.
>
>>[!example]
>> ```csharp
>>  Console.WriteLine(10 / 3);// quotient will be 3 (integer division)
>>  Console.WriteLine(10 / 0);// This will throw a DivideByZeroException at runtime
>> ```
>>
>
ø