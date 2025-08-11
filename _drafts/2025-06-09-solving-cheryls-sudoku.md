---
layout: post

title: Solving Cheryl's Sudoku
author: mizu
---
A 4x4 sudoku can't be that hard, can it?

*Cheryl's Sudoku* by Elytron is a puzzle that combines sudoku with [Cheryl's Birthday](https://wiki), a famous type logic puzzle in which people make statements about others' knowledge.

The puzzle is shown below. Everything below it will be spoil the answer. If you want to solve it yourself, go do it now.

(puzzle goes here)

Here's how I approached solving this puzzle.

**Disclaimer:** This writeup is an edited summary of the correct solution, not my exact thought process. Actually solving this involved a lot of difficult brainstorming and trial and error, as should be the case with a good puzzle.

A good strategy when solving this type of puzzle is to start with every possible state, then narrow down the states based on each statement until only one possibility remains.

> Albert: "Nobody here can place any digits yet."

What could A be?

Using sudoku rules alone, A must be >= 4 (1+1+2) and <= 11 (4+4+3). However, these sums can only be made one way, letting Albert place the digits immediately. Therefore, A must be between 5 and 10.

Carl has a similar cage. For Albert to be sure that Carl can't place digits, the value of A must be impossible for the scenarios where C is 4 or 11.

If C is 4, then cage A must contain 3 and 4 in the lower cells, and can contain 2 or 3 in the upper cell (it can't be 4, because we already ruled out 4+4+3). This means A cannot be 9 or 10.

If C is 11, then cage A must contain 1 and 2 in the lower cells, and can contain 2 or 3 in the upper cell (it can't be 1, because we already ruled out 1+1+2). This means A cannot be 5 or 6.

Therefore, after Albert's statement, it is now public information that A is 7 or 8.

> Bertrand: "Well, now I can."

Bertrand manages to place one or more digits knowing only B and the fact that A is 7 or 8. Let's figure out how this is possible.

The contents of cage B and cage A are similar. Due to sudoku rules, the two digits in cage B are the two digits in cage A's bottom row. It follows that A = B + (contents of A's top box). 

Bertrand knows these are the only possible contents of cage A (up to order). Only when B is 3 (1+2) or 7 (3+4), Bertrand will know A and be able to place a digit in cage A's top cell.

A = 7
1 2 4
1 3 3
2 2 3

A = 8
1 3 4
2 2 4
2 3 3

B = 3 -> A = 7; top cell = 4

B = 7 -> A = 8; top cell = 1

Therefore, it is now public information that A,B is either 7,3 or 8,7. More specifically, the completed sudoku must include one of the following:

```
. . . .
. 4 . .
1~2 3~4
. . 1~2
```
```
. . . .
. 1 . .
3~4 1~2
. . 3~4
```

> Carl: "No one else was told the same number as I was."

We know from earlier C is between 5 and 10. From this statement, we know it is not 7 or 8. From the fact that Carl does not know D, we know it is not 5 or 6.

This leaves us with 9 and 10.

This state is now no longer possible, because it is incompatible with C being 9 or 10.
```
. . . .
. 1 . .
3~4 1~2
. . 3~4
```

The updated state in the public knowledge looks like this:
```
A = 7
B = 3
C = 9/10
D = 4/5/6
 .   .   .   .
 .  [4] 2/3  .
 1 ~ 2   3 ~ 4
[4] [3]  1 ~ 2
```

> David: "Someone here knows more digits than I do."

A and B are already public knowledge, so Albert and Bertrand cannot know more than others. Therefore, David is saying that Carl knows more than David does (who in turn knows as much or more than Albert and Bertrand).

Since this is the last statement before someone solves the sudoku, Carl must be the one to do so. 

First, let's see what David's statement does to the public knowledge, then focus on Carl's perspective to determine the solution.

If D is 6, then cage D must contain 2 and 4, and David solves the whole sudoku. This makes D=6 impossible.
```
3 2 1 4
1 4 3 2
2 1 4 3
4 3 2 1
```
If D is 4, then cage D must contain 1 and 3, and David knows 9 digits:
```
 .  1/2 [4] 1/3
1/3 [4] [2] 1/3
1/2 1/2 [3] [4]
[4] [3] [1] [2]
```
If D is 5, then cage D can contain 1 and 4, or 2 and 3, and we can assume this does not give many digits.

Let's find a lower bound on the number of digits David knows Carl knows.

If C is 9, then Carl knows 6 digits.
```
 .  1/2 3/4  .
1/3 [4] [2] 1/3
1/2 1/2 3/4 3/4
[4] [3] [1] [2]
```
If C is 10, then Carl knows 6 digits still.
```
 .  1/2 1/2  .
 .  [4] [3]  .
1/2 1/2 [4] [3]
[4] [3] 1/2 1/2
```

So, from David's perspective, Carl can only know 6 digits! This means we can rule out D=4 and D=6, resulting in the following public knowledge:
```
A = 7
B = 3
C = 9/10
D = 5
 .  1/2   . 2/3/4
 .  [4] 2/3 1/2/3
1/2 1/2 3/4  3/4
[4] [3] 1/2  1/2
```