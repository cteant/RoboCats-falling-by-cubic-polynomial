# RoboCats-falling-by-cubic-polynomial

This repository contains the algorithm to solve the IBM puzzles that available at: https://www.research.ibm.com/haifa/ponderthis/challenges/April2016.html

## Puzzles
The interesting puzzle goes as the followings:
Let p(x)=x^3-300*x^2+a*x+b be a cubic polynomial with unknown parameters a and b that has three positive integers roots. 
Based on the surprising fact that cats falling from lower floors have been found to suffer greater injury than those falling from higher floors (http://www.damninteresting.com/high-rise-syndrome), IBM has built a robo-cat that when experimentally dropped from a height of n stories will either disintegrate (if p(n)>=0), or leave the experiment exactly the same way it entered it (if p(n)\<0). 

If you have only seven such robo-cats, find an algorithm to predict the fate of a fall from every floor with no more than 16 experiments. 

## Solution:
We know there are three positive integer solutions, denoted as n1, n2 and n3. To solve this puzzle, we need to find at least two of them. Here are some observations that are useful to solve this puzzle.

* First observation: n1+n2+n3=300
* Second observation: the solutions to p'(x)=0, denoted as x1 and x2, satisfy x1<=100<=x2

We can first try p(100):
* if p(100)>0, then the first robocat die and we know n1<=100<=n2<=n3\<200. We can use 3 robocats to find n1 in the interval of [1,100]. Note that this subproblem is the traditional famous egg dropping problem. By looking up the table (http://datagenetics.com/blog/july22012/index.html) we know that it needs at most 9 experiments to find n1. After we get n1, we can obtain the average of n2 and n3. Then we can use 3 other robocats to find either of them with no more than 6 experiments.
* if p(100)\<0, then we still have 7 robocats and we know n1<=n2<=100<=n3<=300. We can use 4 robocats to find n3 in the interval of [100,300] by no more than 9 experiments. After we get n3, we can obtain the average of n1 and n2. Similarly, the other 3 robocats can be used to find either of them with no more than 6 experiments.
