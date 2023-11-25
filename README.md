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

In the study of stock, it's common to calculate the daily return, definided as the percentual change of the value from one day to the next:

$$ return = \frac{S(t)-S(t-1)}{S(t-1}} $$

The mean $\boldsymbol{\mu}$ and standard deviation $\boldsymbol{\sigma}$ of the returns then constitute an important source of information about the growing trend and the volatility of the stock.

Assuming a risk free scenario, it's common to model stocks by using geometric brownian motion, which states that *the logarithm of the stock follows a brownian motion* (Figure 2) (or a Wiener process; see [Wikipedia](https://en.wikipedia.org/wiki/Wiener_process)). This means that the differential variation of stock (dS) can be related to the diferential time variation (dt) as

$$dS = S(\mu dt + \sigma \epsilon \sqrt{dt}) $$

where $\epsilon=N(0,1)$ is a normally distributed random variable with mean 0 and variance 1. It can be shown (see [here](https://medium.com/@polanitzer/forward-looking-monte-carlo-simulation-predict-the-future-value-of-equity-using-the-lognormal-f54320f9c230)) that this leads the Stock price to be modeled by

$$S(t)=S(0)\exp{(at+b\sqrt{dt})} $$

where $a=\mu-\sigma^2/2$ while $b=\sigma \epsilon$.

![figure2](https://hkilter.com/images/9/99/Brownian-motion.gif)

(Figure 2: Brownian motion describes the random motion of a gas particle)

By repeatedly picking normal random numbers and applying them to the model we can then predict, day by day, the behaviour of stock. The trend and volatility ($\mu$ and $\sigma$) of the data can be calculated from the historical data available online.

## The dataset

We use in this project Apple's historical data ([Yahoo](https://finance.yahoo.com/quote/AAPL/)) for 5 years, starting from Nov 23, 2018 to Nov 22, 2023 (Figure 3).

![figure3](https://github.com/rafael-raiser/portfolio_montecarlo/blob/main/AAPL_stock.png)

(Figure 3: Apple's historical data)

## Results

The first step of the analysis is determining the mean and standard deviation of the returns. We calculate $\mu=0.14\% day^{-1}$ and $\sigma=2.06\% day^{-1/2}$. Figure 4 shows a histogram of the returns.

![figure4](https://github.com/rafael-raiser/portfolio_montecarlo/blob/main/returns_hist.png)

(Figure 4: Histogram of the returns)

We then perform Monte Carlo simulation to evaluate the stock after T=252 days from the last value of $S_0=191.31$ using 100,000 repetitions. The result is plotted in figure 5.

![figure5](https://github.com/rafael-raiser/portfolio_montecarlo/blob/main/results_hist.png)

(Figure 5: Monte Carlo results)

The resulting distribution obtained is the so called log-normal distrubution, a pdf for which the logarithm of its values are normally distributed.

In a deterministic world where there's no volatility and the stock follows $S(t)=S(0)\exp{(\mu t)}$, the stock after 252 days would be **272.18**. This value is close to the mean of the Monte Carlo results. **272.39**, whose standard deviation is **91.38**.

