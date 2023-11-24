# Monte Carlo simulation applied to finances

**Skills**: pandas, numpy, data analysis, data science, statistics, stocks, finances, equity

## Abstract

In this project we apply Monte Carlo method to simulate the evolution of Apple's stock given a list containing historical data to be used as reference and an initial value.

## Monte Carlo simulation

Monte Carlo simulation is a method to predict the outcome of a stochastic (random) process. It works by repeatedly picking random values from a given probability distribution, applying them to the model and calcating the result. After many repetitions, one gets the frequency at which each outcome can happen.

A simple example is shooting dice. After a sufficient large number of rolls, there'll be an approximately equal number of results for each one of the six faces. This happens because the probability of each outcome is equal to 1/6:

$$P(x=1)=...=p(x=6)=1/6 $$

The dice outcome is an example of discrete probability. This can be extended to the a continuous variable (x) by defining the probability density function f(x) (pdf); then, the probability of finding an outcome in the interval $[x_1 , x_2]$ is given by an integral

$$P({x_1} < x < {x_2})=\int_{x_1}^{x_2} f(x) dx $$

![figure1]()

(Figure 1: Monte Carlo method applied to approximating the value of pi)

A important step of every Monte Carlo simulation is random sampling, the process of getting a random value for a variable given its pdf. In computation, this is done by first picking a random uniformly distributed number r between 0 and 1 (see [Wikipedia](https://en.wikipedia.org/wiki/Pseudorandom_number_generator)) for which the pdf is simply f(x)=1 when 0<x<1.

In the example of a dice roll, we could say that the roll result is 1 if we pick a random nuber r for which $0<r\leq 1/6$, 2 if $1/6<r\leq 2/6$ and so on. To get a random number for an arbitrary pdf, we can use the fact that these probability densities are all normalized: $\int_\mathbb{R} f(x) = 1$. So, we can write

$$ \int_{0}^r 1 dx = \int_{-\infty}^x f(x')dx'=F(x) $$

where F(x) is the cumulative distribution function (cdf).

Therefore the sampling from a given pdf can be done by calculating its inverse and applying it to a uniform random number:

$$ F(x)=r \implies x=F^{-1}(r) $$



## Stocks

## Results
