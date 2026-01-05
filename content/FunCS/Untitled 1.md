---
draft: true
---

# Section 2: Sequential vs. Chained Branches - Point Calculation

## Stage 1: Analyzing Sequential Branches
Focus: Understanding how multiple if-statements execute in sequence.

### Paper Task:
Analyze this code:
```csharp
int points = 0;
bool hasSolvedPuzzle = true;
bool hasFoundKey = true;

if (hasSolvedPuzzle)
{
    points = points + 5;
}
if (hasFoundKey)
{
    points = points + 3;
}
```

For each line number, fill in the state of variables immediately AFTER that line executes:

State Table (when both conditions are true):
| After Line | points | hasSolvedPuzzle | hasFoundKey | Notes (what happened & why) |
|------------|--------|-----------------|-------------|----------------------------|
| 1          |        |                 |             |                            |
| 2          |        |                 |             |                            |
| 3          |        |                 |             |                            |
| 7          |        |                 |             |                            |
| 11         |        |                 |             |                            |

### Coding Task:
1. Create SequentialPoints.cs
2. Implement the code above
3. Add after each points change:
   ```csharp
   Console.WriteLine($"Points after check: {points}");
   ```
4. Run and verify your state table predictions
5. Add assertions to verify final points value:
   ```csharp
   Debug.Assert(points == 8, "Both true should give 8 points");
   ```

## Stage 2: Analyzing Chained Branches
Focus: Understanding how else-if chains affect execution.

### Paper Task:
Analyze this alternative code:
```csharp
int points = 0;
bool hasSolvedPuzzle = true;
bool hasFoundKey = true;

if (hasSolvedPuzzle && hasFoundKey)
{
    points = points + 8;
}
else if (hasSolvedPuzzle)
{
    points = points + 5;
}
else if (hasFoundKey)
{
    points = points + 3;
}
```

For each line number, fill in the state of variables immediately AFTER that line executes:

State Table (same conditions):
| After Line | points | hasSolvedPuzzle | hasFoundKey | Notes (what happened & why) |
|------------|--------|-----------------|-------------|----------------------------|
| 1          |        |                 |             |                            |
| 2          |        |                 |             |                            |
| 3          |        |                 |             |                            |
| 7          |        |                 |             |                            |

### Coding Task:
6. Create ChainedPoints.cs
7. Implement the code above
8. Add the same print statements
9. Compare execution to your predictions
10. Document key differences from sequential version

## Stage 3: Design Your Own Comparison
Focus: Creating and analyzing different branching approaches.

### Paper Task:
Design two versions of a damage calculation system:
11. Sequential version that:
   - Adds fire damage (2 points) if target is burning
   - Adds frost damage (3 points) if target is frozen
   - Adds weakness bonus (double damage) if target is weak

12. Chained version that:
   - Handles all combinations in a single chain
   - Ensures consistent results
   - Prevents double-counting

For each version:
- Write complete code
- Create state tables
- Predict outcomes for key scenarios
- Explain why you organized the branches this way

### Coding Task:
13. Create a new project for damage calculation:
   ```bash
   # Navigate to your lab folder
   cd ~/1301/Lab_branching
   
   # Create a new project directory
   mkdir DamageCalc
   cd DamageCalc
   
   # Initialize new C# project
   dotnet new console
   
   # Open Program.cs in your editor
   # Replace the existing code with your solution
   ```
14. Implement both versions
15. Add print statements showing damage calculations
16. Test with these scenarios:
   - Only burning
   - Burning and frozen
   - All conditions true
17. Compare results between versions
18. Document which approach was better and why

## Reflection Questions
19. When would you use sequential if-statements?
20. When would you use chained if-statements?
21. How does the order of conditions matter in each approach?
22. What happens when multiple conditions are true in each version?

## Key Concepts to Review
- Sequential if-statements can execute multiple times
- Chained if-else statements execute exactly once
- Condition order affects chained but not sequential branches
- Complex conditions might be clearer in one form vs the other