# Score-Based Tic-Tac-Toe

You will create a tic-tac-toe game where the goal is to achieve a certain amount of points faster than your oppenent. Alternatively, there are cases where the game ends early and the player with the higher score until then wins.

## Main Idea

The game starts with a normal 3x3 tic-tac-toe board. When a player left-clicks on an empty cell, they place their mark there, alternating between "X" and "O". When they right-click however, the place a nested grid inside the cell instead without any mark in it. At every nesting level, the score from a placed mark is counted differently:

- On the highest level, you get 1 point for every mark.
- On the second level, you get 0.5 points for every mark.
- On the third level, you get 0.25 points for every mark.
  Etc.

If you get three in a row on any level, you get (winning multiplier)⋅(typical level points) instead of just the typical level points. This is not for the marks themselves, but for the whole field. The marks in a field which has been won by a player or which has reached a stalemate are either counted or not. If not, all points made by marks and sub-fields in the field are lost for both players when the field is won. This behaviour has to be entered as a setting before the game starts. The same goes for the winning multiplier, it also has to be entered as a setting before the game starts. Additionally, the maximum number of nestings possible also has to be entered as a setting before the game starts. Same goes for the number of points needed to win.

Because the player who starts first has an edge, the second player also gets the points made for the first mark of the game.

## Example Game

Starting settings:

- Maximum nesting level: 2
- Points needed to win: 5
- Winning multiplier: 3
- Marks in won or stalemated fields are counted: yes
- First-move compensation: second player receives the points of the first mark

Starting board (level 1), scores X=0, O=0:

```
+---+---+---+
|   |   |   |
+---+---+---+
|   |   |   |
+---+---+---+
|   |   |   |
+---+---+---+
```

Turn 1 (X left-clicks top-left, level 1 mark):

- X gains 1 point (level 1 mark).
- O also gains 1 point (first-move compensation).
  Scores: X=1, O=1

Board now:

```
+---+---+---+
| X |   |   |
+---+---+---+
|   |   |   |
+---+---+---+
|   |   |   |
+---+---+---+
```

Turn 2 (O right-clicks center, creates nested field id 101):

- No points yet (no mark was placed).

Board now:

```
+---+---+---+
| X |   |   |
+---+---+---+
|   |101|   |
+---+---+---+
|   |   |   |
+---+---+---+
```

Field 101 is shown here:

```
- 101 -
+
+
```

Turn 3 (X plays inside field 101, top-left of level 2):

- X gains 0.5 points (level 2 mark).
  Scores: X=1.5, O=1

Field 101 now:

```
- 101 -
+---+---+---+
| X |   |   |
+---+---+---+
|   |   |   |
+---+---+---+
|   |   |   |
+---+---+---+
```

Turn 4 (O plays inside field 101, center of level 2):

- O gains 0.5 points.
  Scores: X=1.5, O=1.5

Turn 5 (X plays inside field 101, top-middle of level 2):

- X gains 0.5 points.
  Scores: X=2.0, O=1.5

Turn 6 (O plays inside field 101, bottom-right of level 2):

- O gains 0.5 points.
  Scores: X=2.0, O=2.0

Turn 7 (X plays inside field 101, top-right of level 2):

- X completes three in a row on level 2.
- Instead of the usual 0.5, X gains (winning multiplier) ⋅ (level 2 points) = 3 ⋅ 0.5 = 1.5.
- Because won fields are counted, the makrs made in field 101 are NOT lost after the win. The last mark counts also, which counts for 0.5 points.
  Scores: X=4.0, O=2.0

Field 101 now:

```
- 101 -
+---+---+---+
| X | X | X |
+---+---+---+
|   | O |   |
+---+---+---+
|   |   | O |
+---+---+---+
```

Turn 8 (O left-clicks bottom-right, level 1 mark):

- O gains 1 point (level 1 mark).
  Scores: X=4.0, O=3.0

Board now:

```
+---+---+---+
| X |   |   |
+---+---+---+
|   |101|   |
+---+---+---+
|   |   | O |
+---+---+---+
```

Turn 9 (X left-clicks top-middle, level 1 mark):

- X gains 1 point (level 1 mark).
  Scores: X=5.0, O=3.0

Board now:

```
+---+---+---+
| X | X |   |
+---+---+---+
|   |101|   |
+---+---+---+
|   |   | O |
+---+---+---+
```

Game end:

- X reached 5 points (points needed to win) on Turn 9.
- The game ends immediately and X wins.

## Functional Requirements

- You have to use the starter code provided and with that, all the tech that we have used thus far (SQLite, EFCore, Angular, ASP.Net, etc.).
- You have to create a REST api using ASP.Net and a frontend using Angular.
- You have to use the auto-generated angular api services!!

<br>

- After every turn, the game should be stored in the database. You can choose your database entities as you want.
- The game should be playable by two players on the same computer.
- Bonus: Implement an AI player (do this last, because the exercise itself is very complex).
- Implement a parser for the game board which adds an existing game to the databsae. The logic for the parser must be implemented as in [parsing-logic.md](parsing-logic.md).
- You can decide whether only one game is shown and that game is overwritten when a new game is imported via the parser, or whether the player chooses what game they are playing from a list of all games on the left side of the screen and parsing adds an additional game.
- The game parser must be accessable from the frontend. In the frontend, there must be a separate page in which you can paste the content of the file to parse into a textarea and a button to parse. You have to show clear error messages when the parsing fails and a success message when the parsing succeeds. The error messages must be very precise so that the user knows where the error to fix is.
- Because the logic code is very complex, you must create at least 5 unit tests testing the logic and the logic only.
