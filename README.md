# Symbolic Regression with Genetic-Programming

In this experiment we were tasked with implementing symbolic regression to find optimal functions associated with 2
data sets: one with a single input variable and one with 3
input variables. We generated 2 genetic programs to fit equations to each data set. In our process, we researched and implemented established techniques of symbolic regression and
genetic programming to construct an efficient and optimal experiment. Our results found adequate equations mapping to
each data set. Experimental techniques varied from the first
data set to the second; the later data set required non-linear
scaling to find an equation with an appropriate fitness.

## Introduction
Genetic programming is a methodology which takes in a
high-level problem statement, and creates its own computer
program to solve that problem. Symbolic regression — an
application of genetic programming — has been explored in
depth by researchers such as John Koza who use the technique to solve challenging optimization problems. Our task
was to implement a genetic program to fit functions with
provided input sets of 25,000 data points. One data set corresponded to a function of a single variable while the other
matched to a 3-variable function.
The paper is organized as follows. Our background section discusses relevant information related to symbolic regression as well as our techniques of data fitting. The experiments section describes the process of our trials as well
as methods used to combat the aforementioned problems of
symbolic regression. In the results section we analyze our
data and compare it with our expectations preceding the experiment. Our conclusion summarizes our findings and discusses further applications of symbolic regression.

## Background
Our experiment relied on established techniques to run efficiently and combat errors encountered during genetic programming. One problem associated with genetic programming is overfitting — finding an equation which matches
tightly to the inputted values from the data, but fails to adequately match outputs omitted from the experiment. The
reader is referred to our experiments section for a further
description of our techniques to combat overfitting. Another
crucial element to genetic programming is the size of seed
populations; in our experiments section we will explain our
techniques related to generating initial trees. Other problems faced in genetic programming include bloat and loss of
diversity, both of which we will cover later.
To simplify the range of the second data set we regularized the data, running the experiment with the log of the yvalues as opposed to the y-values themselves. We will cover
this technique of non-linear scaling in both the experiments
and results sections.

