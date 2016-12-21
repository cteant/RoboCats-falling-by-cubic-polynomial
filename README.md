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
* Second observation: the solutions to p\'(x)=0, denoted as x1 and x2, satisfy x1<=100<=x2
