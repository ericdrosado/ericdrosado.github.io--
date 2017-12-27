<h2> Intro </h2>
Adding features to an app or even refactoring for that matter can be a difficult task. Lately, I've been trying to apply as much as I can from my readings as well as discussions I have had with my mentors and fellow apprentices. With that, I would like to share a recent experience I had with adding a new feature to my Tic-Tac-Toe application.

<h2> The New Feature </h2>
The new feature was a very simple feature. The ultimate goal was to relabel my board cells starting with the number 1 instead of 0. Here is the before and the after images below:

Before:
![](/assets/posts/2017-12-27-reflection-on-adding-a-feature-to-tic-tac-toe/board_before.png){class="img-responsive"}

After: 
![](/assets/posts/2017-12-27-reflection-on-adding-a-feature-to-tic-tac-toe/board_after.png){class="img-responsive"}

Now, on the surface, this feature seems straightforward, but it becomes difficult when your board logic is tied to how a player and computer makes a move. 

<h2> Initial Analysis </h2>
Given that other parts of my code would have to change with the change of my board I initially started to make the necessary changes where they were needed. So, after changing the array which held my board:

Before:
```
private string[] gameBoard = {"0", "1", "2", "3", "4", "5", "6", "7", "8"};
```
After:
```
private string[] gameBoard = {"1", "2", "3", "4", "5", "6", "7", "8", "9"};
```

I knew that my player and computer logic would have to change how a move was placed. This was my first mistake.

Player Move Logic:
```c#
public int GetMove(string[] board) {
            string input = this.io.GetInput();
	    while (!this.validateInput.IsInputOnBoard(input, board) || !this.validateInput.IsInputNumericString(input)) {
                IncorrectInputView(board);
                input = this.io.GetInput();
            
	    }
            int move = Int32.Parse(input);
            return move;
        
}
```

Let's just focus on the player move logic first as it is the simplest to understand. Here you will see that a player can input a value for a move. This input is validated on whether it is a value on the board and if it is a numeric string. If that passes then the value is converted into and integer and returned, which is eventually sent to the Board class to place a move:

```c#
public void UpdateBoard(int move) {
    gameBoard[move] = currentMarker;
    SwitchMarker();
}
```

Now, notice here that once the move is chosen, that value is used as the index in the board array. So if someone chose "0" as their board placement, by the time it made it to the UpdateBoard method, that choice is used as the index to change the "0" on the board to the current marker, which would be the "X" symbol for a player.

This becomes problematic when the board changes it's labeling. Why? Well, if a player now chooses "1," the 1 index is not the first cell, but in fact the second cell. With the current logic kept intact, the board would look like this if 1 was chosen in this new labeling scheme:

![](/assets/posts/2017-12-27-reflection-on-adding-a-feature-to-tic-tac-toe/one_chosen.png){class="img-responsive"}

That is obviously not what we want. So, the simple immediate fix that came to my mind is to subtract one from the players choice in the GetMove method. The biggest issue with this is, now my GetMove method and the Class that it is in, will have knowledge about my board and it's Board Class. So this is a huge NO, NO! Besides, this also has the ability to fail some tests as well with this change. So, that option is not an option. Board Logic, must stay within the Board Class. So, here was my remedy to the issue:

```
public void UpdateBoard(int move) {
            gameBoard[move - BoardIndexAdjustment] = currentMarker;
            SwitchMarker();
        
}
``` 

Now, the move is properly indexed with a Constant called BoardIndexAdjustment, which is equal to "1." I chose to use a constant here, because if I simply just did "move - 1," it may not immediately be clear to the reader of this code what the "1" is doing.

<h2> The MiniMax Issue </h2>
The largest issue was much further down the line with the AI logic. The AI relies heavily on the correct board indexing.

![](/assets/posts/2017-12-27-reflection-on-adding-a-feature-to-tic-tac-toe/minmax_before.png){class="img-responsive"}

 A simple subtract one from the move choice will not allow this to be a clean change. This process needed some additional refactoring. Available spaces will grab all the literal values that are not symbols, but numbers. So if spaces 1, 2, and 3 are open, those values will be returned and not the index value on the gameboard. So, when the section of code above does this bit:
```
gameBoardCopy[availableSpaces.ElementAt(i)] = marker;
```
The ```availableSpaces.ElementAt(i)``` is not the correct index value for the gameboard, similar to the problem of our player move. This time though, we don't have the luxury of an UpdateBoard method to utilize here as the MiniMax algorithm does it's recursion. If we left the code as is it would throw a "StackOverflow" error.

The issue lies in allowing the board to choose the right index, but allowing the move choice to be an available space as the move will be adjusted once it gets to the UpdateBoard method. This was my solution:

```
for (int i = 0; i < availableSpaces.Count; i++) {
                Moves moveValues = new Moves();
                moveValues.Spot = availableSpaces.ElementAt(i);
                string[] gameBoardCopy = (string[]) gameBoard.Clone();
                int index = Array.IndexOf(gameBoardCopy, moveValues.Spot.ToString());
                gameBoardCopy[index] = marker;
                int score = GetBestMove(gameBoardCopy, AlternateMarker(marker)).Score;
                moveValues.Score = score;
                moves.Add(moveValues);
            
}
```

Notice that ```moveValues.Spot = availableSpaces.ElementAt(i)``` stays the same. This is intentional because when the move is returned from ComputerLogic class to the Board Class, the UpdateBoard method will correct the index. The big difference here is that the correct index for the move is chosen using the following: 

```
int index = Array.IndexOf(gameBoardCopy, moveValues.Spot.ToString());
gameBoardCopy[index] = marker;
```

Now, I will no longer have a StackOverflow Error, and the best move that is returned will be correctly indexed in the Board Class.

<h2> A Sudden Realization </h2> 
As of writing this, it just occurred to me that I can use the same logic in my MiniMax algorithm to finding the correct index in my BoardClass, which would effectively remove the constant. Now my UpdateBoard method can look like this:

```
public void UpdateBoard(int move) {
            int index = Array.IndexOf(gameBoard, move.ToString());
            gameBoard[index] = currentMarker;
            SwitchMarker();
        
}
```

<h2> Conclusion </h2>
A thing that I did not mention is that I wanted to initially change how my gameBoard was initialized, but i remembered Sandi Metz in that one should not change code anticipating the future during a refactor. Instead, it is better to focus on the task at hand.

The other piece of knowledge I utilized is the idea of separating knowledge between my classes. If I initially went with subtracting one from the move of my player to get the correct index, my player move method would know too much about the Board Class, which can create many other issues down the road. 
 
I find that reflecting on your choices and applying the knowledge you have learned can truly help in keeping your code clean. It is clear, especially at the end of this post, that reflection can yield some amazing benefits, which in turn could lead to cleaner code. 
