>[!abstract] Variables
>
>>[!Definition]
>>
>>A *Variable* is a reserved space in memory used to store a value of some type.
>
>When we want to label a value in programming, we usually create a variable for it. We refer to giving a value to this variable as *binding* or *assigning* the value to it.
>
>>[!info] Properties
>>
>>- Memory Management: Types define the exact amount of memory space needed for each variable, allowing C# to efficiently allocate and manage computer resources
>>- Program Reliability: Fixed types prevent unexpected behavior by ensuring operations (like division) consistently work as intended across your code 
>
>>[!example]
>>```csharp
>> int x = 7; // reads: create an int variable called x, and assign 7 to it.
>>```
>
>Notice that we use the `=` symbol here. In C# `=` is used for *assignment*, where is `==` is used to check for *equality*.

> [!DEFINITION] Type Safety
> The guarantee that operations will behave consistently based on their types, preventing unexpected bugs and crashes.

>[!abstract] Scope
>
>>[!Definition]
>>
>>Program *scope* hold boundaries of code, with a defined *start* and *end*, where any new entries to the programs state are cleared once execution crosses the *end*.
>
>This means that any variable, or other binding, we create within a specific scope is *only* accessible within, and *inaccessible* from the outside.
>>[!example]
>>In C#, we use *curly braces* `{}` to define the bounds of scope.
>>```csharp
>>{
>>int x = 17;
>>x > 1; // this works
>>}
>>
>>{
>>int y = 18
>>y = x; // this doesn't, x doesn't exist outside of the scope it belongs to
>>}
>>```

>[!abstract] State
>
>>[!Definition]
>>
>>Program *state* is the set of *bindings* at a given point of execution.
>
>We can refer to the set of variables and their current values as our *bindings*.
>>[!example]
>>Given the following program
>>```csharp
>>int x = 37;
>>int y = 12;
>>bool isBigger = false;
>>
>>isBigger = x <= y;
>>
>>x = 12
>>isBigger = x <= y; 
>>```
>>After line 1 runs, 37 is bound by x.
>>After line 2, 12 is bound by y.
>>Depending on if we check after line 3 or line 8 runs, isBigger will be either false or true respectively.
>>
>>To handle this we introduce using a table to track the program state:
>>
>>
| after line # runs | x   | y   | isBigger |
| ----------------- | --- | --- | -------- |
| 1                 | 37  | - | -     |
| 2                 | 37  | 12  | -      |
| 3                 | 37  | 12  | false    |
| 5                 | 37  | 12  | false    |
| 7                 | 12  | 12  | false    |
| 8                 | 12  | 12  | true     |