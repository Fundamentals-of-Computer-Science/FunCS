---
title: Ch. 1.2 - Numbers
draft: true
aliases:
  - numbers
---

Having explored Boolean algebra, now we can venture back to more familiar territory: working with numbers!

There are two primary types of number we will consider in this course:
1. Whole numbers, what we will be referring to as *integers*,
2. Floating point numbers, of which we will mainly use the *double* type.

In this chapter we will cover both: showing how computers handle each, along with the operators we need consider when working with them.

## Integers

Have you ever struggled to solve a problem, only to realize that you were looking too closely for a solution, when really you didn't understand the problem? This is all to common: it's human nature to solve puzzles and see patterns. However sometimes we must fight this nature, instead focussing on bringing these problems to a simple, concrete form. Once this is done, solving them becomes easy; once reduced to a simple form, our brains love solving them for us. Again I iterate: solutions fall from well defined problems. So when we talk about representing problems, often times we can reduce them to numbers. One common shape that problems commonly fall to are whole numbers. How many years until 2089? How many cents in a dollar? How many reps/sets while lifting should I perform? All of these break down to a whole number answer.

To represent these numbers in C#, we introduce the *int* type. 

>[!abstract]
>
>>[!Definition] 
>>An Int (integer) is a whole number, who's value is between -2,147,483,648 and 2,147,483,647.
>


Now you may wonder why this range specifically: it represents of the possible integers you can fit in 32 bits of memory, centered around 0. Notice that it includes negative numbers, C# similarly has a 32-bit whole number type which represents the natural numbers, that is, only 0 and positive numbers.

> [!Definition] uint (unsigned Int)
> An unsigned int is a positive whole number which is a value between 0 and 4,294,967,295.

You can look at the comprehensive list of integer types supported in C# here: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types. I encourage you to read about them, however we will stick strictly to *int* and *uint* in this course.

### Integer Operations

While you may be familiar with the operators below, they are a bit different than you may be used to. When working with integers we must carefully consider the limitations of being a whole number.


>[!abstract] Addition of Integers
>
>>[!definition] Addition
>>
>> $Add: (int, int) \rightarrow int$ returns the sum of two integers.
>
>>[!property] Properties of Addition
>> - **Overflow:** If the sum exceeds `int.MaxValue`, overflow occurs, wrapping around to `int.MinValue`.
>
>>[!example]
>> ```csharp
>>  int x = 5;
>>  int y = 10;
>>  int sum = x + y;        // sum will be 15
>>  int overflow = int.MaxValue + 1; // overflow will be int.MinValue (-2147483648)
>> ```

>[!abstract] Subtraction of Integers
>
>>[!definition] Subtraction
>>
>> $Subtract: (int, int) \rightarrow int$ returns the difference between two integers.
>>
>
>>[!property] Properties of Subtraction
>> - **Underflow:** If the difference is less than `int.MinValue`, underflow occurs, wrapping around to `int.MaxValue`.
>
>>[!example]
>> ```csharp
>>  int x = 5;
>>  int y = 10;
>>  int difference = x - y; // difference will be -5
>>  int underflow = int.MinValue - 1; // underflow will be int.MaxValue (2147483647)
>> ```


The main change to keep in mind is how underflow and overflow work. More formally, one could say:
	If we define Int.MaxValue as the upper range, 2,147,483,647, and Int.MinValue as the lower end, -2,147,483,648. Then if we overflow by n, the resulting value will be Int.MinValue + n. Conversely, if we *underflow* by n, the resulting value will be Int.MaxValue - n.

Let’s do some exercises to test your understanding:

> [!exercise] Overflow
> TODO


> [!Exercise] Underflow
> TODO


---

Now let’s move on to Multiplication and Division, which we will split up for reasons you will see.


>[!abstract] Multiplication of Integers
>
>>[!definition] Multiplication
>>
>> $Multiply: (int, int) \rightarrow int$ returns the product of two integers.
>
>>[!property] Properties of Multiplication
>> - **Overflow/Underflow:** Overflow or underflow can occur if the product is outside the range of `int.MinValue` to `int.MaxValue`.
>
>>[!example]
>> ```csharp
>>  int a = 10;
>>  int b = 3;
>>  int product = a * b;      // product will be 30
>>  int overflow = int.MaxValue * 2; // overflow will occur
>> ```

Just to check how you are with over/underflow with multiplication, do the following exercises on your own.

> [!exercise] Overflow
> TODO

> [!Exercise] Underflow
> TODO

This is all pretty close to what you’ll have experienced in any algebra course before. However, let’s talk about something a little different: Division

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
>>  int a = 10;
>>  int b = 3;
>>  int quotient = a / b;     // quotient will be 3 (integer division)
>>  // int zeroDiv = a / 0; // This will throw a DivideByZeroException at runtime
>> ```

Let’s explore an example to understand this cutoff thing. If we take the following expression:
`32 / 4 `, this evaluates to `8` like you’d expect. However, this becomes untrue when the numerator is not cleanly divided by its denominator.

Take the following expression: `10 / 3`. In normal algebra over the real numbers, this would return 3.333…, however notice the type signature for integer division: it simplifies to an integer. This means we must have some criteria for picking a value that’s appropriate. Some may think of using a rounding algorithm, such as rounding up if the decimal is equal to or greater than .5, otherwise rounding down. However this can be suboptimal for consistencies sake: therefore we simply drop the decimal point *always*. Therefore with integer division, `10/3` returns `3`.

Run through these exercises to check your understanding:


> [!exercise] Integer Rounding 1
> TODO

> [!exercise] Integer Rounding 2
> TODO

> [!exercise] Integer Rounding 3
> TODO

---

There is one final operator for division we must cover, commonly called the remainder operator. It serves to find the remainder of dividing two values. A common use for it is taking an integer expression and finding a result which fits within a desired range. We’ll discuss this more later when we cover [[Arrays]].


>[!abstract] Modulus of Integers
>
>>[!definition] Modulus
>>
>> $Mod: (int, int) \rightarrow int$ returns the remainder of a division between two integers.
>>
>
>>[!property] Properties of Modulus
>> - **Remainder:** The result is always an integer between 0 (inclusive) and the absolute value of the divisor (exclusive).
>> - **Sign:** The sign of the result follows the sign of the dividend (the first operand).
>> - **Division by Zero:** Modulus by zero results in a `DivideByZeroException`.
>
>>[!example]
>> ```csharp
>>  int a = 10;
>>  int b = 3;
>>  int remainder = a % b;  // remainder will be 1 (10 divided by 3 is 3 with a remainder of 1)
>>  int negative = -7 % 3; // remainder will be -1
>>  // int zeroDiv = a % 0; // This will throw a DivideByZeroException at runtime
>> ```


Modulus as an operator is used throughout all sorts of problems in CS. There are two general ways of thinking of taking the remainder: one is the literal: divide the first operand by the second, return the remainder. However some are helped with a clock analogy:

An analog clock serves as mod 12: 

Say it is 2 o-clock. What time is it in 15 hours?
You may internally use mod to see that we only need move the hour hand 3 times to find our answer. But this is the equivalent of moving our hour hand 15 times around the circle.

When using modulus, this is often the style of problems we use it for: we are looking for a value in a cycle or constrained space, so we use modulus to control the range of possible outputs.

---

You will find that most problems we think about in computer science can be represented with *ints*. This is more than an observation: computer memory cannot hold infinite precision, so all fractional values are approximated into a certain number of bits. And it seems like a lot of work to hand transform fractional values into an *integer* representation every time we want a fractional value. Therefore we will instead turn to floating-point types.

## Floating-Point

>[!abstract] Double
>