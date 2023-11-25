# Monte Carlo simulation applied to finances

**Skills**: pandas, numpy, data analysis, data science, statistics, stocks, finances, equity

## Abstract

In this project we apply Monte Carlo method to simulate the evolution of Apple's stock given a list containing historical data to be used as reference.

## Monte Carlo simulation

Monte Carlo simulation is a method to predict the outcome of a stochastic (random) process. It works by repeatedly picking random values from a given probability distribution, applying them to the model and calculating the result. After many repetitions, one gets the frequency at which each outcome happens.

A simple example is shooting dice. After a sufficient large number of rolls, there'll be an approximately equal number of results for each one of the six faces. This happens because the probability of each outcome is equal to 1/6:

$$P(x=1)=...=p(x=6)=1/6 $$

The outcomes of a dice are an example of a discrete probability distribution. The concept can be extended to a continuous variable (x) by defining the probability density function f(x) (pdf) for which the probability obtaining a result between x and x+dx is $dP=f(x)dx$; then, the probability of finding an outcome in the interval $[x_1 , x_2]$ is given by an integral:

$$P({x_1} < x < {x_2})=\int_{x_1}^{x_2} f(x) dx $$

Another example of application of Monte Carlo method is approximating the value of pi (Figure 1). In the first quadrant of the cartesian plane, the equation of a unitary circle centered at the origin is simply $y=\sqrt{1-x^2}$. Since the area of the circle is $A_C = \pi/4$ and the area of the unitary square inside which the circle is inscribed is $A_S = 1$, one can sort many pairs of uniformly distributed random numbers between 0 and 1 assign them to points (x, y); after many repetitions, the number of points inside the circle (satisfying $y<\sqrt{1-x^2}$) $N_{in}$ is compared to the total number of points N to find an approximation for pi:

$$ \frac{N_{in}}{N}=\frac{A_C}{A_S}=\frac{\pi}{4} $$

![figure1](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/Pi_monte_carlo_all.gif/800px-Pi_monte_carlo_all.gif)

(Figure 1: Monte Carlo method applied to approximating the value of pi)

In the previous example, we say an important step of every Monte Carlo simulation: random sampling, the process of getting a random value for a variable given its pdf. In computation, this is done by first picking a random uniformly distributed number r between 0 and 1 (see [Wikipedia](https://en.wikipedia.org/wiki/Pseudorandom_number_generator)) for which the pdf is simply $f(r)=1$ when $0 < r < 1$.

In the example of a dice roll, we could say that the roll result is 1 if we pick a random nuber r for which $0 < r \leq 1/6$, 2 if $1/6 < r \leq 2/6$ and so on. For approximating the value of pi, the coordinates (x, y) are obtained from two uniformly distributed random number between 0 and 1. In general, to get a random sample for an arbitrary pdf f(x), we can use the fact that the probability density is normalized: $\int_{-\infty}^{+\infty} f(x) = 1$. So, we can write

$$ \int_{0}^r 1 dr' = \int_{-\infty}^x f(x')dx'=F(x) $$

where F(x) is the cumulative distribution function (cdf).

Therefore the sampling from a given pdf can be done by calculating its inverse and applying it to a uniform random number:

$$ x=F^{-1}(r) $$


## Stocks

Let's now apply Monte Carlo simulation and the concept of Markov chains in the finance of stocks. A stock consist of all the shares by which ownership of a corporation or company is divided. According to the weak form efficiency, the past movements, volume and earnings data don't affect the future price of a stock. This characterizes stock evolution as a Markov process: all the information needed to predict its value is the present one.

Assuming a risk free scenario, it's common to model stocks by using geometric brownian motion which states that the logarithm of the value follows a brownian motion (or a Wiener process; see [Wikipedia](https://en.wikipedia.org/wiki/Wiener_process)). This means that the differential variation of stock (dS) can be related to the diferential time variation (dt) as

$$dS = S(\mu dt + \sigma \epsilon \sqrt{dt}) $$

where $\epsilon$ is a normally distributed random variable with mean 0 and variance 1, $\mu$ is the $\sigma$ is its standard deviation. It can be shown (see [here](https://medium.com/@polanitzer/forward-looking-monte-carlo-simulation-predict-the-future-value-of-equity-using-the-lognormal-f54320f9c230)) that this leads the stock price 





## The dataset

https://github.com/rafael-raiser/portfolio_montecarlo/blob/main/AAPL_stock.png

## Results

https://github.com/rafael-raiser/portfolio_montecarlo/blob/main/returns_hist.png
https://github.com/rafael-raiser/portfolio_montecarlo/blob/main/log-returns_hist.png

https://github.com/rafael-raiser/portfolio_montecarlo/blob/main/results_hist.png

