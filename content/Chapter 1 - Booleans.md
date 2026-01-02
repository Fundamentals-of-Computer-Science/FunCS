---
title: Chapter 1 - Booleans
draft: false
---

# Chapter 1: Booleans

This is your first chapter of real code. We start with the simplest type: the boolean.

Booleans represent true/false values. Just two possible values, nothing else. This simplicity is deceptive. All problems in computer science ultimately reduce to boolean problems. And all data in computers, when viewed closely enough, is represented by sequences of boolean values: binary numbers, zeros and ones, false and true. Booleans are both the simplest data type we will use and the foundation everything else is built on.

This chapter explores booleans through five sections:

- **Data and Memory:** What booleans are and how we store them
- **Computation:** How we transform boolean values
- **Control Flow:** How booleans determine which code runs
- **Functions:** How we create our own boolean computations
- **Structured Data:** How we group related booleans together

We begin with the fundamentals: what is a boolean, and how do we hold onto one?

---

## Data and Memory

Every chapter in this book starts here: with the data. Before we compute, we understand what we're working with. This section answers two questions: what is this type, and how do we store it?

### Types and Values

In Chapter 0, we described computations by the *kind* of data they use. We wrote things like `length: string → number` to say "length takes a string and produces a number." Now we make "kind" precise.

A **type** is a kind of data. It describes a set of valid values and the restrictions they follow.

A **value** is data that cannot be simplified further. Every value belongs to exactly one type.

These two concepts work together. Types describe categories. Values are the actual data that lives in those categories. The number 5 is a value. It belongs to the number type. The text "hello" is a value. It belongs to the string type.

Now let's meet our first type.

### Booleans

The simplest type is the boolean.

A **boolean** is a type with exactly two valid values: `true` and `false`.

That's it. No other values exist. Not "maybe." Not "unknown." Just `true` and `false`.

Only two values might seem limiting. But this constraint is what makes booleans powerful. Because there are only two possibilities, we can reason about them completely. Every question has a definite answer. Every case can be checked. And because all data in a computer is ultimately sequences of binary values, understanding booleans means understanding the atoms that everything else is made of.

When we wrote `is-negative: number → boolean` in Chapter 0, this is what boolean means. The function takes a number and produces one of two possible values: `true` or `false`.

Booleans answer yes/no questions. Is the user logged in? Is the file ready? Is the number positive? Each of these has a boolean answer.

### Variables and Binding

We have values. Now we need a way to store them so we can use them later.

A **variable** is a named location in memory that holds a value of a specific type.

When we store a value in a variable, we **bind** that value to that name.

Here is our first line of C# code:

```csharp
bool x = true;
```

This creates a boolean variable named x and binds the value true to it.

Let's break that translation down:
- "Create a boolean variable named x" — we're making a new storage location
- "and bind the value true to it" — we're storing true in that location

When we bind a value to a variable, that variable holds that value until we bind a different one, or until the variable leaves scope. (We'll define scope in the Control Flow section.)

---

**Try it yourself.**

Translate this code to English:

```csharp
bool flag = true;
```

Write your answer before revealing ours.

<details>
<summary>Reveal answer</summary>

"Create a boolean variable named flag and bind the value true to it."

</details>

If your answer differed, note what you missed before continuing.

---

### What Happens When Code Runs

Before we go deeper into variables, we need to understand how programs execute.

Programs run line by line, top to bottom. Each line completes before the next one starts. As lines execute, the program's **state** changes.

The program's **state** is the set of bindings at a given point of execution.

Consider this code:

```csharp
bool x = true;
bool y = false;
```

After line 1 runs, x is bound to true. That's the entire state: one variable, one binding.

After line 2 runs, x is still bound to true, and now y is bound to false. The state has grown: two variables, two bindings.

We can visualize state with a table:

| after line | x | y |
|------------|---|---|
| 1 | true | — |
| 2 | true | false |

Each row shows the state after that line executes. The dash means the variable doesn't exist yet.

State tables help us trace what a program does step by step. When your code doesn't behave as expected, and it won't always, tracing state is how you find the problem. You'll think "the variable should be true here" and the table will show you it's actually false. That's the bug. This skill, tracing state, will save you hours of confusion.

### The Mechanism: What `bool flag = true;` Actually Does

Let's look more carefully at what happens when we write `bool flag = true;`

We can break this into tokens and see what each one does:

- `bool` — reserve space in memory for a boolean value
- `bool flag` — name that space "flag"
- `bool flag =` — prepare to bind a value
- `bool flag = true;` — bind the value true to flag

Three discrete actions happen:
1. Reserve space for a boolean
2. Name that space "flag"
3. Bind the value true to that name

This is what "create a variable and bind a value" means at a mechanical level. The computer finds room in memory, labels it with a name, and stores your value there.

---

**Try it yourself.**

Write C# code for this description:

"Create a boolean variable named example_var and bind the value false to it."

<details>
<summary>Reveal answer</summary>

```csharp
bool example_var = false;
```

</details>

If your answer differed, note what you missed before continuing.

---

### Rebinding Variables

Variables can be rebound to new values. That's why they're called *variables*, they can vary.

```csharp
bool x = true;
x = false;
```

Line 1 creates x and binds true to it.

Line 2 rebinds x to false. The old value is gone.

Here's the state table:

| after line | x |
|------------|---|
| 1 | true |
| 2 | false |

The translation for `x = false;` is simply: "Bind the value false to x."

Notice there's no `bool` keyword in line 2. We don't write `bool x = false;` because x already exists. We're rebinding, not creating.

**Common mistake:** Writing `bool x = false;` when x already exists causes an error. The variable already has a name and a place in memory. You just want to change what's stored there, so you write `x = false;` without the type.

### Reading vs Writing

So far we've only bound values to variables. That's writing. What about reading?

Consider this code:

```csharp
bool copy_of_x = x;
```

The right side isn't a literal value like `true` or `false`. It's a variable name. What happens?

When we use a variable in an expression, we **evaluate** it. Evaluating means retrieving the value currently bound to that name.

So `bool copy_of_x = x;` does this:
1. Evaluate x (get the value bound to x)
2. Bind that value to copy_of_x

If x is bound to true, then evaluating x produces true. We then bind true to copy_of_x.

The translation: "Create a boolean variable named copy_of_x and bind the result of evaluating x to it."

This is more precise than saying "copy x into copy_of_x." We're not copying the variable. We're evaluating it to get a value, then binding that value to a new variable.

Let's trace this with a state table:

```csharp
bool x = true;
bool copy_of_x = x;
```

| after line | x | copy_of_x |
|------------|---|-----------|
| 1 | true | — |
| 2 | true | true |

Line 2 evaluates x (gets true), then binds true to copy_of_x. Both variables now hold true, but they're independent bindings.

---

**Try it yourself.**

Translate this code to English:

```csharp
bool done = finished;
```

<details>
<summary>Reveal answer</summary>

"Create a boolean variable named done and bind the result of evaluating finished to it."

</details>

If your answer differed, note what you missed before continuing.

---

### Two Operations, One Symbol

We've now seen two different operations on variables:

**Binding (writing):** Store a value in a variable.
- `x = true;` — bind true to x
- `x = false;` — bind false to x

**Evaluating (reading):** Retrieve the value currently bound.
- Using `x` on the right side of `=` evaluates it

The same variable name means different things depending on where it appears:

```csharp
x = y;
```

On the left of `=`, x is a target. We're binding to it.
On the right of `=`, y is evaluated. We're reading from it.

This is a pattern you'll see everywhere in programming. Left side: where to store. Right side: what to store (which may require evaluation first).

### Value Types

Now let's trace a longer example to see something important:

```csharp
bool x = true;
bool copy_of_x = x;
x = false;
```

State table:

| after line | x | copy_of_x |
|------------|---|-----------|
| 1 | true | — |
| 2 | true | true |
| 3 | false | true |

After line 2, both variables hold true.

After line 3, x holds false, but copy_of_x still holds true.

Why didn't copy_of_x change when we changed x?

Because when we wrote `bool copy_of_x = x;`, we evaluated x to get the value true, then bound that value to copy_of_x. The two variables are independent. Each has its own storage location. Changing one doesn't affect the other.

This behavior is called a **value type**. Booleans are value types. When you assign a value type variable to another variable, you copy the value itself. The two variables don't share anything after that.

Think of it like writing a number on two different pieces of paper. Erasing one paper and writing a new number doesn't change what's on the other paper. Each paper has its own independent copy.

### Observing Values

We can store booleans and track state on paper. But how do we see what's actually bound to a variable when the program runs?

We use Console.WriteLine.

```csharp
Console.WriteLine(x);
```

This displays the value bound to x in the console, the text output area where programs can print messages.

The translation: "Evaluate x and display the result to the console."

Notice the pattern: we evaluate first (get the value), then do something with it (display it).

Console.WriteLine has this type signature:

```
WriteLine: bool → void
```

What's `void`? It means "no value." WriteLine takes a boolean, displays it, and produces nothing in return. It performs an action but doesn't give back data we can bind to a variable.

We'll see void again when we write functions that do things without producing values.

---

**Try it yourself.**

Write code that creates a boolean variable named `active`, binds true to it, then displays its value to the console.

<details>
<summary>Reveal answer</summary>

```csharp
bool active = true;
Console.WriteLine(active);
```

Line 1: "Create a boolean variable named active and bind the value true to it."

Line 2: "Evaluate active and display the result to the console."

</details>

If your answer differed, note what you missed before continuing.

---

### Review

Before continuing, test yourself on what you've learned. Use the protocol from Chapter 0: attempt each exercise from memory, then search the chapter to check your answers, then note what you missed.

#### Part 1: Definitions

Write the definitions from memory, then find them in the chapter to check.

1. What is a **type**?
2. What is a **value**?
3. What is a **boolean**?
4. What is a **variable**?
5. What is **binding**?
6. What is **state**?

If any of your answers differed from the definitions in the chapter, note what you missed and write the corrected version.

#### Part 2: Translations

Translate each line of code to English, then check against the translation patterns shown earlier in this section.

1. `bool ready = false;`
2. `bool status = active;`
3. `done = true;`
4. `Console.WriteLine(finished);`

If any translations differed, note what you missed and write the corrected version.

#### Part 3: Writing Code

Write C# code for each description.

1. Create a boolean variable named `enabled` and bind the value true to it.
2. Bind the value false to an existing variable named `running`.
3. Create a boolean variable named `backup` and bind the result of evaluating `original` to it.

Check your code against the examples in this section. If any differed, note what you missed and write the corrected version.

#### Part 4: State Tables

Complete the state table for this code:

```csharp
bool a = true;
bool b = false;
bool c = a;
a = false;
b = c;
```

| after line | a | b | c |
|------------|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |

Trace through each line using the rules you learned: creating binds a value, using a variable on the right side evaluates it, and reassignment rebinds without affecting other variables (value types are independent). If your table doesn't match what you expect when you trace through carefully, identify where your reasoning went wrong.

---

You now know how to define booleans, create variables, bind and evaluate values, and track program state. In the next section, we'll learn how to transform these values through computation.

## Computation

We can store booleans and track state. Now we want to transform state. What tools do we have to compute new values?

Every type has tools for computation. For numbers, we have arithmetic. For booleans, we have logical operators. This section covers the tools that come built-in for working with boolean values.

### Computation Transforms State

In the previous section, we bound values directly:

```csharp
bool x = true;
```

The value true came from us, typed literally into the code. But what if we want to compute a new value from existing bindings?

```csharp
bool a = true;
bool b = !a;
```

Line 1: bind true to a.

Line 2: evaluate a (get true), compute its negation (get false), bind false to b.

State table:

| after line | a | b |
|------------|---|---|
| 1 | true | — |
| 2 | true | false |

The `!` symbol is an operator. It took a value and transformed it. This is computation.

Here's the key insight: computation reads state (evaluates bindings), transforms values, and the result can be bound to update state. The pattern is always the same. Evaluate, transform, bind.

### Expressions

Before we explore operators, we need one more definition.

An **expression** is code that evaluates to a value.

We've already seen expressions without naming them. When we wrote `bool copy_of_x = x;`, the `x` on the right side is an expression. It evaluates to whatever value x holds.

A literal value like `true` is also an expression. It evaluates to itself.

And when we write `!a`, that's an expression too. It evaluates a, applies the NOT operator, and produces a new value.

Expressions can be simple (a single variable or value) or compound (operators combining multiple parts). But they all share one thing: they evaluate to a value.

The right side of `=` is always an expression. We evaluate it completely, then bind the result.

One more thing: a variable by itself is an expression of its type. If `x` is a boolean variable, then `x` is a boolean expression. It evaluates to a boolean value.

### Logical NOT

Let's examine our first operator.

**NOT** (`!`) is a unary boolean operator with type signature `bool → bool`. It returns false when given true, and true when given false.

NOT takes a boolean and produces a boolean. It transforms true to false, and false to true. We call it negation.

Unary means "one." NOT takes one input.

We can describe NOT's behavior completely with a truth table:

| x | !x |
|---|-----|
| true | false |
| false | true |

Two inputs, two outputs. Every possible case covered. This is the power of booleans: we can enumerate everything.

**Translation:** `!x` reads as "not x."

Let's see NOT in context:

```csharp
bool flag = true;
bool opposite = !flag;
```

Translation for line 2: "Create a boolean variable named opposite and bind the result of evaluating not flag to it."

State table:

| after line | flag | opposite |
|------------|------|----------|
| 1 | true | — |
| 2 | true | false |

Line 2 does three things:
1. Evaluate flag → true
2. Apply NOT to true → false
3. Bind false to opposite

---

**Try it yourself.**

Translate this code to English:

```csharp
bool result = !flag;
```

Write your answer before revealing ours.

<details>
<summary>Reveal answer</summary>

"Create a boolean variable named result and bind the result of evaluating not flag to it."

</details>

If your answer differed, note what you missed before continuing.

---

**Try it yourself.**

Write C# code for this description:

"Create a boolean variable named flipped and bind the negation of done to it."

<details>
<summary>Reveal answer</summary>

```csharp
bool flipped = !done;
```

</details>

If your answer differed, note what you missed before continuing.

---

### Logical AND

What if we want to check whether two things are both true?

**AND** (`&&`) is a binary boolean operator with type signature `(bool, bool) → bool`. It returns true only when both inputs are true. Otherwise, it returns false.

Binary means "two." AND takes two inputs.

Truth table:

| a | b | a && b |
|---|---|--------|
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

Four combinations, four outputs. Only the last row produces true.

**Translation:** `a && b` reads as "a and b."

Let's trace AND in action:

```csharp
bool left = true;
bool right = false;
bool both = left && right;
```

Translation for line 3: "Create a boolean variable named both and bind the result of evaluating left and right to it."

State table:

| after line | left | right | both |
|------------|------|-------|------|
| 1 | true | — | — |
| 2 | true | false | — |
| 3 | true | false | false |

Line 3 does four things:
1. Evaluate left → true
2. Evaluate right → false
3. Apply AND to true and false → false
4. Bind false to both

---

**Try it yourself.**

Translate this code to English:

```csharp
bool ready = loaded && valid;
```

<details>
<summary>Reveal answer</summary>

"Create a boolean variable named ready and bind the result of evaluating loaded and valid to it."

</details>

If your answer differed, note what you missed before continuing.

---

**Try it yourself.**

Write C# code for this description:

"Create a boolean variable named confirmed and bind the result of active and enabled to it."

<details>
<summary>Reveal answer</summary>

```csharp
bool confirmed = active && enabled;
```

</details>

If your answer differed, note what you missed before continuing.

---

### Logical OR

What if we want to check whether at least one of two things is true?

**OR** (`||`) is a binary boolean operator with type signature `(bool, bool) → bool`. It returns true when either input is true, or when both are true. It returns false only when both inputs are false.

Like AND, OR is a binary operator.

Truth table:

| a | b | a \|\| b |
|---|---|----------|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

Only the first row produces false. Any true input makes the whole expression true.

**Translation:** `a || b` reads as "a or b."

Let's trace OR:

```csharp
bool first = false;
bool second = true;
bool either = first || second;
```

State table:

| after line | first | second | either |
|------------|-------|--------|--------|
| 1 | false | — | — |
| 2 | false | true | — |
| 3 | false | true | true |

Line 3 does four things:
1. Evaluate first → false
2. Evaluate second → true
3. Apply OR to false and true → true
4. Bind true to either

---

**Try it yourself.**

Translate this code to English:

```csharp
bool allowed = admin || owner;
```

<details>
<summary>Reveal answer</summary>

"Create a boolean variable named allowed and bind the result of evaluating admin or owner to it."

</details>

If your answer differed, note what you missed before continuing.

---

**Try it yourself.**

Write C# code for this description:

"Create a boolean variable named canProceed and bind the result of ready or override to it."

<details>
<summary>Reveal answer</summary>

```csharp
bool canProceed = ready || override;
```

</details>

If your answer differed, note what you missed before continuing.

---

### Equality Operators

Sometimes we need to check whether two values are the same.

**Equals** (`==`) is a binary operator with type signature `(bool, bool) → bool`. It returns true when both inputs have the same value. Otherwise, it returns false.

**Not Equals** (`!=`) is a binary operator with type signature `(bool, bool) → bool`. It returns true when the inputs have different values. Otherwise, it returns false.

Truth table for `==`:

| a | b | a == b |
|---|---|--------|
| false | false | true |
| false | true | false |
| true | false | false |
| true | true | true |

Equal values produce true. Different values produce false.

Truth table for `!=`:

| a | b | a != b |
|---|---|--------|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | false |

This is the exact opposite of `==`. Different values produce true.

**Translation:** `a == b` reads as "a equals b." `a != b` reads as "a does not equal b."

Note: equality operators work for other types too, not just booleans. We'll revisit them in each chapter as we introduce new types.

---

**Try it yourself.**

Translate this code to English:

```csharp
bool same = x == y;
```

<details>
<summary>Reveal answer</summary>

"Create a boolean variable named same and bind the result of evaluating x equals y to it."

</details>

If your answer differed, note what you missed before continuing.

---

**Try it yourself.**

Write C# code for this description:

"Create a boolean variable named different and bind the result of comparing whether expected does not equal actual to it."

<details>
<summary>Reveal answer</summary>

```csharp
bool different = expected != actual;
```

</details>

If your answer differed, note what you missed before continuing.

---

### Compound Expressions

We can chain operators to build larger expressions.

Consider:

```csharp
bool result = true && false || true;
```

This expression has two operators. Which one applies first?

Like arithmetic has order of operations (multiplication before addition), boolean operators have precedence:

1. NOT (`!`) — highest priority, applies first
2. AND (`&&`) — middle priority
3. OR (`||`) — lowest priority, applies last

So `true && false || true` means:
1. First, apply AND: `true && false` → `false`
2. Then, apply OR: `false || true` → `true`

The result is `true`.

Let's trace a more complex expression:

```
!true || false && true
```

Step by step:
1. Apply NOT first: `!true` → `false`
2. Now we have: `false || false && true`
3. Apply AND next: `false && true` → `false`
4. Now we have: `false || false`
5. Apply OR last: `false || false` → `false`

The entire expression evaluates to `false`.

Parentheses override precedence. Whatever is inside parentheses evaluates first:

```
!(true || false) && true
```

Step by step:
1. Evaluate inside parentheses: `true || false` → `true`
2. Apply NOT: `!true` → `false`
3. Apply AND: `false && true` → `false`

Without parentheses, `!true || false && true` would evaluate differently (as we showed above). Parentheses let you control the order explicitly.

When in doubt, use parentheses. They make your intent clear to both the computer and anyone reading your code.

---

**Try it yourself.**

Evaluate this expression step by step:

```
true || false && false
```

<details>
<summary>Reveal answer</summary>

1. AND has higher precedence than OR, so: `false && false` → `false`
2. Now we have: `true || false`
3. Apply OR: `true || false` → `true`

Result: `true`

</details>

If your answer differed, note what you missed before continuing.

---

**Try it yourself.**

Evaluate this expression step by step:

```
!false && !true || false
```

<details>
<summary>Reveal answer</summary>

1. Apply NOT operators first: `!false` → `true`, `!true` → `false`
2. Now we have: `true && false || false`
3. Apply AND: `true && false` → `false`
4. Now we have: `false || false`
5. Apply OR: `false || false` → `false`

Result: `false`

</details>

If your answer differed, note what you missed before continuing.

---

### Short-Circuit Evaluation

There's one more thing to know about AND and OR: they don't always evaluate both sides.

Consider:

```csharp
bool result = false && something;
```

AND returns true only when both sides are true. If the left side is false, the result is false no matter what the right side is. So C# doesn't bother evaluating the right side. It already knows the answer.

This is called short-circuit evaluation.

The rules:

- `false && anything` → `false` (right side never evaluated)
- `true || anything` → `true` (right side never evaluated)

For AND: if the left side is false, stop. The answer is false.

For OR: if the left side is true, stop. The answer is true.

Why does this matter? For now, it's an optimization. The program skips work it doesn't need to do. Later, when we learn about functions that have side effects, short-circuit evaluation becomes important for correctness, not just efficiency. We'll revisit this.

---

**Try it yourself.**

In the following expression, which parts actually get evaluated?

```csharp
bool result = true || (false && true);
```

<details>
<summary>Reveal answer</summary>

Only `true` on the left side of `||` gets evaluated.

Because the left side of OR is true, the entire OR expression is true. C# never evaluates `(false && true)`.

</details>

If your answer differed, note what you missed before continuing.

---

### Review

Before continuing, test yourself on what you've learned. Attempt each exercise from memory, then search the chapter to check your answers.

#### Part 1: Definitions

Write the definitions from memory, then find them in the section to check.

1. What is an **expression**?
2. What is **NOT** (`!`)? Include its type signature.
3. What is **AND** (`&&`)? Include its type signature.
4. What is **OR** (`||`)? Include its type signature.
5. What is **Equals** (`==`)? Include its type signature.

If any of your answers differed from the definitions in this section, note what you missed and write the corrected version.

#### Part 2: Truth Tables

Complete these truth tables from memory:

**NOT:**

| x | !x |
|---|-----|
| true | |
| false | |

**AND:**

| a | b | a && b |
|---|---|--------|
| false | false | |
| false | true | |
| true | false | |
| true | true | |

**OR:**

| a | b | a \|\| b |
|---|---|----------|
| false | false | |
| false | true | |
| true | false | |
| true | true | |

Check your tables against the ones in this section.

#### Part 3: Translations

Translate each line of code to English.

1. `bool inverted = !original;`
2. `bool both = first && second;`
3. `bool any = x || y || z;`
4. `bool match = input == expected;`

Check your translations against the patterns in this section.

#### Part 4: Evaluate Expressions

Evaluate each expression step by step. Show your work.

1. `!false || true`
2. `true && false || true && true`
3. `!(true && false) || false`
4. `false || !false && true`

Work through each one, then trace through using the precedence rules to verify.

#### Part 5: Short-Circuit

For each expression, identify which parts get evaluated.

1. `false && (true || false)`
2. `true || (false && true)`
3. `true && false || true`

Think carefully about when evaluation stops.

---

You now know how to transform boolean values through computation. You can negate, combine, compare, and build compound expressions. In the next section, we'll see how these boolean expressions control which code runs.