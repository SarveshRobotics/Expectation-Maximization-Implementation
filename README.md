# Expectation-Maximization-Implementation
Implementing EM Algorithm on noisy data-sets. #Python

## Problem Statement
The purpose of this problem is to implement the Expectation-Maximization algorithm for the problem of grouping points into lines. That is, we assume that we are given a set of points, and we want to find two lines that explain them. In the expectation step, we find the line that minimizes the weighted sum of squares distance from points to
lines. The variance is estimated using the distance between each line and the points. In the maximization step we assign (probabilistically) each point to each line based on its distance to the lines.

1. Line Fitting (20 points) Write a function that fits a line to data. Note that Weiss describes a method for doing this using weighted least squares, which essentially only looks at error in the y direction. This fits the examples below,in which noise is added to the y coordinate. If you are interested, you can also implement, for a small amount of extra credit, a total least squares method, that takes account of the Euclidean distance between each point and the line, and see what difference this makes. You will have to do a little research to see how this works. Test your function with the following set of points:

  (i) x=0:0.05:1; y=2*x+1;
  (ii) x=0:0.05:1; y=2*x+1+0.1*randn(size(x));
  (iii) x=0:0.05:1; y=(abs(x-0.5) < 0.25).*(x+1)+(abs(x-0.5) >=0.25).*(-x);
  
  In all cases plot the data and the best fitting lines.
  
  
 2. E-M (80 points) Write a function that estimates the parameters of two lines using E-M. It should get as input vectors x,y and return (a1,b1,c1), (a2,b2,c2) the parameters of the two lines as well as the weight vectors w_1 and w_2. (Set the free parameter in Eq. (2) and (3), sigma^2=0.1.) You must figure out how to initialize E-M appropriately, and how to set other parameters, if any. You should be able to manage things to that the algorithm converges to a reasonable answer.
  a. Test your function on the data in part (iii) of the previous question. Plot the data and the two fitted lines  as estimated after each of the first five iterations. Also, show in separate plots the membership vectors after every iteration.
  b. Experiment with adding Gaussian noise to the y coordinates. How much noise can you add before the algorithm breaks? Describe your experiment and illustrate with appropriate plot(s).
  

------------------------------------------------------------------------------------------------------------------

Suppose we are given a set of datapoints that were generated by multiple processes, for example two lines. We need to estimate two things: (1) the parameters (slope and intercept) of the two lines and (2) the assignment of each datapoint to the process that generated it. The intuition behind EM is that each of these steps is easy assuming the
other one is solved. That is, assuming we know the assignment of each datapoint, then we can estimate the parameters of each line by taking into consideration only those points assigned to it. Likewise, if we know the parameters of the lines we can assign each point to the line that fits it best.

This gives the basic structure of an EM algorithm:
  1. start with random parameter values for the two models.
  2. Iterate until parameter values converge:
    (i) E step: assign points to the model that fits it best.
    (ii) M step: update the parameters of the models using only points assigned to it.
   

    
