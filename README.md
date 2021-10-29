# A-B-testing
A/B testing project for Udacity
This project was a write up about formulating, excuting and analyzing an A/B test on a sample set of webpage users data to see if a new design change positively impacts the website.


# The Importance of Lienarity in Finance
Nonlinear dynamics are important but lienar models are employed because they are easity to use.  In finance, linea rmodels are widely used to help price securities and perform optimal portfolio allocation. One significant aspect of lienarity in financial modeling is its assurance that a problem terminates at a globally-optimal solution

We can describe the problem of portfolio allocation as a system of lienar equations, containing either equalities or inequalities.  These linear systems can then be represented in a matrix form as $Ax=B$ where $A$ is our known coefficient value, $B$ is the observed result, and $x$ is the vecotr of values that we want to find out. 

# The Capital Asset Pricing Model and the Security Market Line

In the famous CAPM, the relationship between risk and rates of return in a security is described as:

$$ R_i = R_f + \Beta_i(E[R_{mkt}] - R_f)$$

The return of a security $i$ is designated as $R_i$ with a beta of $\B_i$.  The CAPM defines the return of the security as the sum of the risk free rate $R_f$ and the multiplication of its beta with the risk premium.  The risk premium can be thought of as the market portfolio's excess returns exclusive of the risk-free rate.  

Beta is a measure of the systematic risk of a stock - a risk that can't be diversified away.  A stock with a beta of 1 indicates that the stock moves perfectly with the market.  A beta of 0 means the stock produces no exces returns regardless of the direction the market moves in.  

The CAPM model measures the relationship between risk and stock returns for every stock in the portfolio basket.  Combinations of optimal portfolios lie along a line called the efficient frontier

There exists a straight line drawn from the market portfolio to the risk free rate.  This line is called the **Capital Market Line (CML)**.  The CML can be thoguht of as the highest Sharpe ratio available among all the other sharpe ratios 

Another line of interest in CAPM is the **Security Market Line (SML)**.  The SML plots the asset's expected return against its beta.  (Return is the Y axis, and Beta is the X-axis).  You draw a line that cross the intersection of $R_i$ and $B_i$ and meets at the y-axis point of the risk free rate.  That diagonal line is the security market line.  Any security priced above the SML is undervalued. 

```
#Linear Regression with Scipy
from scipy import stats

stock_returns = [0.065,0.0265,-0.593,-0.001, 0.0346]
mkt_returns = [0.055, -0.09, -0.041, 0.054, 0.22]
beta, alpha, r_value, p_value, std_err = stats.linregress(stock_returns, mkt_returns)

```
- Alpha is the intercept
- Beta is the slope
- p-value is the hyptohesis test of the null hypothesis of a zero slope,
- r-value = correlation coefficient
- std_err = standard error of the estimate.

# The Arbitrage PRicing Theory Model

The CAPM suffers from several limitations like the use of a mean-variance framework and the fact that returns are captured by just one risk factor - the market risk only.  In a well diversified portfolio, the unsystematic risk of various stocks cancel out and is essentially eliminated

The **Arbitrage Pricing Theory (APT) Model** was put forward to address these shortcoming and offers a general approach of determining the asset prices other than the mean and variances.

THE APT model assumes that the security returns are generated accoridng to multiple factor models, which consist of a lienar combo of several systematic risk factors.  Such factors could be the inflation rate, GDP growth rate, real interest rates, or dividends

$$ E[R_i] = \alpha_i + \Beta_{i,1}F_1 + \Beta_{i,2}F_2 + ... + \Beta_{i,j}F_j$$

So this is a multivariate linear regression.

In this example, we will use the `ols` function of `statsmodels` to perform ordinary least squares regression to videw its summary

# Nonlinearity in Finance
Practitioners in the financial industry use nonlinear models to forecast volatility, price derivatives, and compute **Value at Risk VAR)**. Unlike linear models, where lienar algebra is used to find a solution, nonlinear models do not necessarily infer a global optima.  Numerical root-finding mehtods are usually employed to converge towards the nearest local optima

## Nonlinearity modeling
$$ f(a+b) \neq f(a) + f(b)$$

# The implied volatility model
Perhaps one of the most widely-studied option-pricing models is the Black-Scholes model.  A clal option is a right, but not an obligation to buy the undelrying security at a particular price and time.  A put option is the right to sell  the security at a particular price and time.  The Black-Scholes model helps determine the fair price of an option with the assumption that the returns of the underlying security are normally distribution or that asset prices are log-normally distributed. 

The formula takes the following assumed varialbes:
- strike price $K$
- time to expiry $T$
- risk free rate $r$
- volatility of undelrying returns $\sigma$
- current price of the underlying asset $S$
- yield $q$

The mathematical formula for a call option, $C(S,t)$ is represented as follows

$$ C(S,t) = Se^{qT} N(d_1) - Ke^{-rT} N(d_2)$$

$$ d_1 = \frac{ln(S/K) + (r - q + \sigma^2 /2)T}{\sigma \sqrt{T}}$$

By way of market forces, the price of an option may deviate from the price that's been derived from Black-Scholes.  In particular, the realized volatility (the observed) could differe from the volatility value as implied by the black-scholes which is indicated by $\sigma$

With volatility being such an important factor in security pricing, many volatility models have been proposed.  One such model is the implied volatility modeling of option prices. 

Suppose we plot the implied volatility values of an equity option given by the Black-Scholes formula with a particular maturity for every strike price available.  In general,, we get a curve common known as a volatility smile

The **implied volatility** typically is at its highest for deep in-the-money and out-of-the-money options.

- **in-the-money**: a call option is considered ITM when its strike price is below the market price.  A put is ITM when strike price is above the market price.  ITM options have an intrinsic value when exercised
- **out-of-the-money**:  A call option is OTM when strike is above market.  A put is OTM when strike is below market.  OTM options have no intrinsic value when exercised, but may still have time value
- **at-the-money (ATM)**:  an option is ATM when a strike price is the same as market price.  ATM options have no intrinsic value but may still have time value

From the preceding volatility curve, one of the objectives in implied volatility modeling is to seek the lowest implied volatility value possible or, in other words, to find the root.  When found, the theoretical price of an ATM option for a particular maturity can be deduced and compared against market prices for opportunities.  

# The Markov Regime-Switching Model

To model nonlinear behavior in economic and financial time series, Markov switching models can be used to characterize time series in different states of the world or regimes.  The ability to transition between these structures lets the model capture complex dynamic patterns.

The Markov property of stock prices implies that only the present values are relevant for predicting the future.  Past stock-price movements are irrelevant ot the way the present has emerged.

Let's take an example of a Markov regime-switching model with $m=2$ regimes:
- $y_t = x_1 + \epsilon_t$ when $s_t = 1$
- $y_t = x_2 + \epsilon_t$ when $s_t = 2$

The application of Markov switching models includes representing the real GDP growth rate and inflation rate dynamics.  These models in turn drive the valuation models of interest-rate derivatives. The probability of switching from the previous state, $i$ to the currrent state, $j$, can be written as:

$$P \[s_t = j| s_{t-1}=i\]$$

# The Threshold Autoregressive Model
One popular class of nonlinear time series models is the threshold autoregressive (TAR) model, which looks very similar to the Markov switching models.  Using regression methods, simple AR models are arguably the most popular models to explain nonlinear behavior.  Regimes in the threshold model are determined by past, $d$ values of its own time series, relative to a threshold value, $c$.

The following is an example of a **self-exciting TAR (SETAR)** model.  The SETAR model is self-exciting because switching between different regimes depends on the past values of its own time series
- $y_t = a_1 + b_1 y_{t-d} + \epsilon_t$ if $y_{t-d} \leq c$
- $y_t = a_2 + b_2 y_{t-d} + \epsilon_t$ if $y_{t-d} > c$

# Smooth transition models
Abrupt regime changes in the threshold models appear to be unrealistic against real-world dynamics.  This problem can be overcome by introducing a smoothly changing continuous function from one regime to another.  The SETAR model becomes a **logistic smooth transition threshold autoregressive (LSTAR)** model with the logistic function shown below

$$G(y_{t-1}; \gamma, c) = \frac{1}{ 1+ e^{-\gamma(y_{t-d} - c)}}$$

The $\gamma$ parameter controls the smooth ransition from one regime to another.  For large values of $\gamma$, the transition is the fastest, as $y_{t-d}$ approaches the threshold variable, $c$.  When $\gamma=0$, the LSTAR model is equivalent ot a simple AR(1) one-regime model.

# Root-finding Algorithms
The use of numerical methods, such as root finding algos, can help us find the roots of a continuous function $f$ such that $f(x)=0$, which can either be the max or the min of the function.  In general, an equation may either contain a number of roots or none at all.

One example of the use of root-finding methods on nonlinear models is the Black-Scholes implied volatility modeling.  An option trader would be interested in deriving implied prices based on the Black-Scholes model and comparing them with market prices.  We will see how we can combine a root finding method wit ha numerical option pricing procedure to create an implied volatility model based on the market prices of a particular option.

Root-finding methods use an iterative routine that requires a start point or the estimation of the root.  The estimation of the root can either converge toward a solution, converge to a root that is not sought, or may not even find a solution at all.  This it is crucial to find a good approximation to the root.  

A bunch of scipy stuff happens after this point.

# Numerical Methods for Pricing Models
A derivative is a contract whose payoff depends on the value of some underlying asset.  In cases where closed-form derivative pricing may be complex or even impossible, numerical procedures excel.  A numerical procedure is the use of iterative computational methods in attempting to converge to a solution.  One such implementation is a binomial tree.  In a binomial tree, a node represents the state of an asset at a certain point in time associated with a price.  Each node leads to two other nodes in the next time step.  Similarly, in a trinomial tree, each node leads to 3 other nodes in the next time step.  However increasing the number of nodes, increases the computational resources.  Lattice pricing attempts to solve this problem by storing only the new info at each time step while reusing shit when possible.

In finite difference pricing, the nodes can also be represented as a grid.  The terminal values on the grid consist of terminal conditions while the edges of the grid represent boundary conditions in asset pricing.  We will discuss the explicit method, implicit method, and the Crank-Nicolson method of the finite difference schemes to determine the price of an asset.

Although vanilla options and certain exotics such as European barrier options and lookback options can be found to have a closed-form solution, other exotic products such as Asian options do not contain a closed-form solution.  In these cases, the pricing of options can be used with numerical procedures.

## Intro to Options

- **Call Option** - right to buy
- **Put Option** - right to sell
- **European option** - can only be exercised on the maturity date
- **American Option** - may be exercised at any time throughout the lifetime of the option

# Binomial trees in option pricing
In the binomial option pricing model, the underlying security at one time period, represented as a node with a given price, is assumed to traverse to two other nodes in the next time step representing an up state and a down state.  Since options are derivatives of the underlying asset, the binomial pricing model tracks the underlying conditions on a discrete-time basis.  Binomial option pricing can be used to value European, American, and Bermudan options.  