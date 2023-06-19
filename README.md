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

## Experiments
Our experiment runs in the following order. First, we generate a base population. In the first experiment on data set
1, we initialize 100 random trees as our seed population. To
generate our initial seed populations for both data sets, we
began by generating the tree’s root node with a randomly selected operator from {+, −, ÷, ×}. From here, each tree is randomly grown by generating leaf nodes with possible values
of operators or integers/real numbers. Once all leaf nodes
are numbers, the growth is terminated and the tree is added
to the seed population. The program then evaluates each tree
and its associated expression, passing through the fittest 50
to use in the subsequent generation. Here, our explanation
calls for a description of the evaluation method. The program checks the function against each input from the data
set and compares that output with the output in the training
set. We use the mean squared error between the resulting
values from the trees and the 20,000 associated outputs from
the testing data set to determine a function’s fitness. Later,
the program uses a complexity score to differentiate between
functions of similar fitness, with priority given to trees with
lesser nodes. The program ranks trees on their evaluation
score (sum of mean squared error and complexity score),
and uses crossover to generate 70 new trees and regenerates
and mutates 15 for a total of 100 new trees in a generation.
Our algorithm more likely will mutate, crossover and regenerate the fitter trees; the program assigns weights to each tree
based on their fitness and then “randomly” selects trees proportionally to their evaluation score. This process repeats for
50 generations, storing the most fit functions — those with
an evaluation score below 1 — in a global table. The program compares these equations to the outputs of the 5,000
data points in the testing set, returning the fittest individual
based on evaluation score.
In order to limit the complexity and bloat of our trees,
we implemented a complexity metric that was added to our
mean squared error value when determining the most fit individuals. Our complexity was calculated with the following formula: n
.5 where n is the number of nodes in a given
tree. For data set 2, we also added a condition that penalized
a given expression more depending on how many variables
from {x1, x2, x3} were present. Although we used this simple
complexity metric, there are more advanced ways to limit
the complexity of expressions in symbolic regression such
as the SymTree heuristic2
and the neat-GP heuristic3
. Given
time restraints, we chose a simpler method for limiting complexity and bloat, however, these more researched methods
would most likely increase the simplicity of resulting symbolic regressions from our experiment.
The experiment on the second data set mimics the run on
the first. However, we changed parameters; we ran the experiment on a seed population of 300 individuals, picking
the fittest 200 trees, and running for 50 generations. The proportions of crossover, mutation, and regeneration stayed the
same, as well as the method for choosing which processes
run on each tree. The largest change comes from our evaluation threshold; we now add trees to a global table when
their fitness score is less than 10. This value comes from errors in previous trials where evaluation scores would plateau
around 5, 4 greater than the then-required epsilon value of 1
from the experiment on the first data set.
Splitting the data into a “training set” and a “testing set”
helps solve the issue of overfitting mentioned earlier; we
ran the experiment with 20,000 data points and tested our
most fit functions on the remaining 5,000, where the program would then return the most fit equation after the final
test.
Loss of diversity presented a serious problem in early trials. We initially ran the experiment with small seed populations of just 4 individuals. This limitation led to few substantial mutations and oftentimes repeated crossovers — meaning our subsequent generations minimally differed from previous generations and evaluation scores barely dropped as
the experiment progressed. Augmenting the size of our population increased the possibilities for tree evolution. For example, choosing the 50 fittest individuals out of a 100-tree
population allows for 50 choose 2 pairings for the crossover
method while choosing just 2 trees from a population of
size 4 offers only a single pairing for crossing over. While
larger generations mean longer running times per evolutionary step, increased choices means the program converges on
fitter functions earlier.

## Results
In the first data set, our output trees gave us fitness scores
around 0.0006. Visually, the equations matched the inputs
and outputs from the csv file. As seen in figure 2, the red
line (the function generated from the program) and the blue
dots (the outputs from the data set) have nearly the same
minima and cross the y-axis around the same point. Figure 1
displays the top three expressions based on fitness and complexity. The fittest functions vary slightly, but all of them
have a (−3+x) term multiplied by another term with a power
of 1, and therefore all expressions are parabolas. The complexities varied slightly more than the fitness values, but all
returned expressions that have complexity values between
3.3 and 3.9. Our best function simplifies down to:
x
2 − 6x + 14
.
Expression Fitness Complexity
x+((-3+x)*(-3+x))-(-5+x) 0.0006 3.605
x+((-4+x)*(-3+x))-(-2) 0.0006 3.317
x+(((-3+x)*(-3+x))-(-2+(-3+x)) 0.0006 3.873
Figure 1: A table of the fittest functions
The functions found from running the genetic program on
the second data set varied slightly more than the first. Unfortunately given the multiple variables, we cannot display
a graph comparing our functions with the outputs from the
csv file. The top five fittest functions from our trials had fitness scores ranging from 2.7 to 3. The complexities varied
less than those functions from experimentation on data set
1, from 4.1 to 4.3. The smaller range suggests that the complexity of the second data set required consistently larger
trees to compute an accurate regression, while smaller errors
allowed for trees of varying size to all accurately represent
the outputs from data set 1. The best expression retrieved
from the algorithm was
(((1.44+((x3)/((x2)∗(x1))))+(3.32+((x3)/(−2.20))))−(0.12−1.48))
which simplifies to
x3
x2 · x1
+
x3
−2.2
+ 6.12
However, because we ran the experiment on the log of the
output values from data set 2, the expression is actually
e
x3
x2
·x1
+
x3
−2.7
+6.12

## Conclusion
Our trees were both accurate and simple. The program returned functions with low complexity scores. This simplicity suggests that our complexity test works, eliminating overly complicated trees through the generations and
leaving us with trees of less depth and without redundant
terms. The low complexity scores could also show the merit
of our bloat-limiting techniques. We also found interesting
how the program returned different functions on each run of
the experiment, yet the evaluation scores were nearly equal.
Likely, the difference in expression comes from varied seed
populations as the fittest trees from the start will uniquely
crossover and converge to a similar yet distinct final tree.
Our project prompts some avenues for further research.
The fitness values for the equations representing the second
data set plateaued in the single-digits. Why does that happen? In what conditions do fitness values plateau? Experimenting with data sets and their various sizes and complexities could find where and why certain symbolic regression
algorithms plateau.
