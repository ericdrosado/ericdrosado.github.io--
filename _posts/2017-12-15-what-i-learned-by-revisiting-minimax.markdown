<h2> Intro </h2>
I have mentioned in a previous blog that I have been working on a command line based Tic-Tac-Toe. This past week I was able to get the project into a working game with an unbeatable AI, but I must humbly admit that the minimax algorithm had revealed some very large weaknesses in my understanding of the magic of objects.  

After rereading my first minimax <a href="https://ericdrosado.github.io/2017/09/12/an-explanation-of-the-minimax-algorithm.html">blog</a>, post, which explains every major detail of the algorithm, I've found that I may have ignored one major piece of the puzzle, which is the use of supporting objects. Of course there were other aspects of the algorithm that I had forgotten about, but this was easily something I did not understand well.

In this post I look to dissect what went wrong during my transcribing of the minimax algorithm from JS, dynamic, to C#, static. 

<h2> MiniMax: The Beginning </h2>
When I first started researching the minimax algorithm, I read a wide variety of explanations. On paper, the logic seemed very straightforward. In fact, I thought I could easily implement my own version of the algorithm without looking at code samples. I found myself trying to reinvent the wheel, and failing miserably in the process. Of course, I caved, and I started to look at a wide variety of code samples. Out of all those samples I settled on one that to me was very clear in it's delivery. I understood the big picture of what each piece of code was trying to do, and I was able to build the pieces one by one to a greater understanding.

<h2> Where I Missed the Mark </h2>
Let's look at the recursion bit of the JS code sample:
```javascript
var moves = [];
for (var i = 0; i < availableSpots.length; i++) {
    var moveValues = {};
    moveValues.spot = availableSpots[i];
    var gameBoardCopy = gameBoard.slice();
    gameBoardCopy[availableSpots[i]] = marker;
    var result = ComputerLogic.prototype.minimax(gameBoardCopy, depth + 1, marker === "O" ? "X":"O");
    moveValues.score = result.score;
    moves.push(moveValues);
  
}
```

Here is the moment where I ran into my largest issue. As I was troubshooting my C# version, I noticed that in some instances the function was returning a move, and not a score. For some reason this baffled me. What I have found as a particular weakness of my understanding was the use of objects to store both the move and score during the traversal of the game tree. Each recursive call to "minimax" is waiting for a score value to be returned. Once the score is returned the remaining code of my minimax function begins:

```javascript
var bestMove;
if(marker === "O") {
    var max = -1000;
    for(var i = 0; i < moves.length; i++) {
	    if (moves[i].score > max) {
        max = moves[i].score;
        bestMove = i;
      
	    }
    
    }
  
} else {
    var min = 1000;
    for(var i = 0; i < moves.length; i++) {
	    if (moves[i].score < min) {
        min = moves[i].score;
        bestMove = i;
      
	    }
    
    }
  
}
  return moves[bestMove];
}
```

To insure that a score is returned, I used an object in my JS version. Notice the object "moveValues," when the score is returned into result, the result.score is stored into the moveValues object, which can be found here:

```javascript
var result = ComputerLogic.prototype.minimax(gameBoardCopy, depth + 1,marker === "O" ? "X":"O");
moveValues.score = result.score;
```

I was able to use javascript object notation in my scoring function, which allowed me to return scores as opposed to moves. So, when I call result.score, I expect to receive a score from result and not a move that was also returned from "moves[bestMove]." 

<h2> Conclusion </h2> 
The power of objects alluded me during my C# implementation. Once I had a handle on this idea I was able to create my own objects that could hold both a move and score attribute and save them. Once these scores are saved they are passed up the recursion, and I ultimately receive the best move possible. 
