<h2> Intro </h2>
Utilizing the minimax algorithm for a zero-sum game can help immensely, but it is very possible to outgrow your powerful algorithm. For instance, I have been recently tasked with creating a 4x4 tic-tac-toe board. My minimax algorithm, as it stands, can not comb through each and every move of such a large board in a minimal amount of time. So, the partial solution to such a problem is to not comb through each and every move by utilizing alpha-beta pruning.

Alpha-beta pruning is a process that decreases the amount of branches that minimax explores, by a method of comparing the maximizer and minimizer values, where the maximizer is represented by a value alpha, the best score for the maximizer given it's respective route down a subtree, and the minimizer is represented by a value beta, the best score for the minimizer given it's respective route down a subtree.

Definitions aside, let's explore a tree in order to understand how this process works.

<h2> The Game Tree </h2>
For this blog post we will look at the following game tree, which is nearing the end of gameplay.

![](/assets/posts/2018-01-02-alpha-beta-pruning-in-minimax/full_tree.png)

If we think of a tic-tac-toe game, you can think of this tree as the maximizer, in my case my AI, is trying to choose the best move. The moves are denoted with scores of 3, 6, and 5. Now, we are getting ahead of ourselves with the scores, but I just wanted the reader to have a visual understanding of what I am talking about.

<h2> Evaluating a Branch </h2>
Moving forward I will be talking about the branch furthest to the left, which is the branch that has the score of 3, and can be seen below:

![](/assets/posts/2018-01-02-alpha-beta-pruning-in-minimax/left_branch.png)

Now, I would like you to imagine that the scores labeled on this branch are gone besides the ones at the bottom of the branch, which are 5, 6, 7, 4, and 5. Next, I would like you to think about starting from the highest point of the tree. At the highest point of the tree the alpha value for the maximizer is -infinity and the beta value for the minimizer is +infinity. Remember that the maximizer is trying to maximize the values it receives, meaning it wants values that are more positive, while the minimizer is the opposite, thus the reason why the initial alpha and beta scores are the extremes of what the maximizer and minimizer do not want. 

As we start to traverse downwards on the left most side of the left branch starting at the min row, which has the score of 3 at the top, the AI will continue to pass down the alpha and beta values until it finds an endgame condition such as a win or tie. Let's travel to the minimizer row that has the score of 5 in the circle. Right below this circle we have some end game conditions, which give the scores 5 and 6. Now, as we traverse down to the end game condition with the score of 5, we are coming in from the minimizer perspective, meaning the minimizer is going to choose the lowest score. In this case, the score is chooses will be represented as beta. In this case, beta will equal five once it reaches the end game condition. Now, this is where the alpha-beta pruning evaluation begins. Here, since beta has been set to 5 it will now be evaluated against alpha, which is still -infinity. If Beta is less than alpha, minimax will not go down the next branch. In this case Beta, 5, is greater than alpha, -infinity, thus the next branch is explored with the score of 6.

<h2> Pruning </h2>
Let's traverse back up to the 5 of the maximizer row. Here is the left branch image reposted for your convenience:

![](/assets/posts/2018-01-02-alpha-beta-pruning-in-minimax/left_branch.png)
 
Now if we travel down the branch to the minimizer row, labeled with a 4, we have three end game conditions with scores of 7, 4, and 5. Of course these scores have not been explored yet so let's work our way from left to right for each endgame condition. Here, the first endgame condition yields 7 and returns that back to the minimizer. Beta is now 7 and alpha is now equal to 5, which is the highest score alpha was able to obtain from the tree. Here beta is evaluated with alpha to see whether or not it will explore the next branch. Since beta is not less than alpha, it will continue to explore the next win condition. 

Now we are at the endgame condition with a 4. Beta is now set to 4 since it is the smallest value between 7 and 4. Here beta is evaluated against alpha and beta is in fact less than alpha, so the next branch of score "5" is not explored and the score of 4 is passed up. 

At this point the maximizer is obviously going to choose the higher value between 4 and 5, thus the reason why the maximizer is labeled with 5. 

<h2> Conclusion </h2>
We can stop at this point as the process will continue from branch to branch implementing minimax as well as alpha-beta pruning. But notice on the farthest branch to the right that we are able to cut a huge bit of the tree using alpha-beta pruning:

![](/assets/posts/2018-01-02-alpha-beta-pruning-in-minimax/right_branch.png)

This can help with optimizing our AI speed, especially for boards larger than 3x3. I would highly recommend implementing this technique for any minimax algorithm. 
