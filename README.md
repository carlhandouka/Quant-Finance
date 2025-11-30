# Personal Projects

Python projects in quantitative finance, including portfolio optimization, algorithmic trading, and ML-based market modeling.

The implemented trading strategies remain simple and clear. I implementred them based on books I cite in the sources' section in the end of this document

## Hedging using Forwards and Futures

Hedging using Futures and Forward contracts are based on a simple idea: Take a position in a derivative that offsets the price risk in the underlying asset

### The logic of hedging
A hedge is designed to lock in a future price.

1. Long Hedge (protect against price increases): Use when you plan to buy the asset later. \
 One should then take a long position in futures/forwards today.

2. Short Hedge (protect against price decreases): Use when you plan to sell the asset later. \
 One should then take a short position in futures/forwards today.

### Ratio of Hedging
1. If the asset you plan to sell/buy is the same the asset on which the Futures/Forward contracts on lying on, the hedge ratio is equal to 1. This is a perfect hedge because this way you can hedge your entire exposure.

2. If this is not case:  Cross-Hedging
We look for Minimum Variance Hedge Ratio: Assumption: $\Delta S$ = a + b $\Delta F$ + $\epsilon$ (where $\Delta S$ and $\Delta F$ are the variations of prices of the spot and futures prices) \
If h is the hedge ratio:   $\Delta S$ - h $\Delta F$= a + (b-h) $\Delta F$ + $\epsilon$ \
Minimum Variance is obtained when $h^{\*}$=b. Here b is the slope of the Linear Regression of $\Delta S$ versus $\Delta F$. \
Finally, $h^{\*}$ = $\rho$ $\frac{\sigma_{S}}{\sigma_{F}}$.  Where $\rho$ is the coefficient of correlation R-squared.\
The optimal number of contracts is $N^{\*}$= $h^{\*}$ $\frac{Q_A}{Q_F}$ \
Where $Q_A$ is the size of the position being hedged, $Q_F$ the size of one futures contract

#### One-day Hedges
$h^{\*}$= $\hat{\rho}$ $\frac{\hat{\sigma_{S}} S}{\hat{\sigma_{F}}F}$ \
where $\hat{\sigma_{S}} S$ and $\hat{\sigma_{F}} F$ are standard deviations for one day.\
Therefore, the optimal number of contracts is $N^{\*}$= $h^{\*}$ $\frac{Q_A}{Q_F}$ = $\hat{\rho}$ $\frac{\hat{\sigma_{S}} S}{\hat{\sigma_{F}}F}$ $\frac{Q_A}{Q_F}$ 

#### Tailing the hedge

If one wants to consider the risk-free rate of interest r in hedging: the optimal number of contracts is therefore $N^{*}$/(1+r)

#### Hedging an Equity Portfolio
For a perfect hedge, $N^{*}$= $\frac{V_A}{V_F}$ where $V_A$ is the current value of the ptf and $V_F$ is the current value of one futures contract.  \
This is the case where the portfolio mirrors the index: $\beta$=1 

More generally, $\beta$ is the sensitivity to index movements 

To hedge a portfolio of sensitivity $\beta$ (not equal to 1): $N^{\*}$= $\beta$ $\frac{V_A}{V_F}$

Here $\beta$ is the slope of the Linear Regression of the index movements versus the portfolio movements.

#### Changing the Beta of a Portfolio

If you want to change the Beta of a ptf to make more/less sensitive to index movements, you can use Futures/Forwards as well. 

To change Beta from $\beta$ to $\beta^{\*}$ ($\beta$ > $\beta^{\*}$ ): \
Short $N^{\*}$= ($\beta$ - $\beta^{\*}$) $\frac{V_A}{V_F}$ contracts 

To change Beta from $\beta$ to $\beta^{\*}$ ($\beta$ < $\beta^{\*}$ ): \
Long $N^{\*}$= ($\beta^{\*}$ - $\beta$) $\frac{V_A}{V_F}$ contracts 

## Interest rates

## Binomial model and no-arbitrage


### Reference rates

Usually, LIBOR (London Interbank Offered rate) was the reference rate. But now that it is no longer active, other reference rates have replaced it. 

They depend on the country you consider the deal in, and they are called Overnight rates. They are now offered by banks that have a surplus of funds with the central ban, called federal funds rate. \
One of the most important reference rates is the SOFR (Secured Overnight Financing Rate). It is the reference rate offered by the Federal Reserve Bank of New York.\
In Europe, it is ESTER (unsecured rate). \
We regard SOFR, and all the overnight rates in general, as risk-free rates of interest since they are backward-looking rates.

### Measuring Risk-free Rate

The annual rate of interest depends on its compounding (monthly, annually, quarterly, daily, ...) but also on the continuity of compounding. Note that continuous compounding is used in algorithms for practical reasons. 

If A is the invested amount at rate R for n years at annual compounding, in n years you'll have: A $(1+R)^{n}$ \
In general, if it is compounded m times per annum, you'll have A $(1+ \frac{R}{m})^{nm}$. 

In continuous compounding, you have: A $e^{Rn}$.

To know more about rates converting, see the Interest Rates section.



## Pricing Forwards and Futures prices

$S_0$ : price of the asset underlying the Futures contract today \
$F_0$ : Futures price today \
r : Zero-coupon risk-free rate of interest per annum (continuous compounding) \
T : time until delivery date in the Futures contract (in years)

### For a no_dividend paying investment asset

We have $F_0$= $S_0$ $e^{rT}$.  
If the equality doesn't hold, arbitrageurs can take advantage of the situation: see Arbitrage section

### Known income investment asset

In this case, one should take the known income I into consideration. \
Therefore, $F_0$= ($S_0$ - I) $e^{rT}$ 

### Known Yield investment asset

We consider that the yield q, is proportional to $S_0$. 
So that, $F_0$= $S_0$ $e^{(r-q)T}$.

### Valuing Forward contracts

f: value of the contract today\
K: delivery price for a contract that was negotiated some time ago

At the beginning: K= $F_0$ , f=0 \
Then, at time t, f=($F_0$ - K) $e^{-rT}$ = $S_0$ - K $e^{-rT}$ . This value can be positive or negative with $S_0$ (or $F_0$ ) value changing over time and K staying the same\
Similarly, for a known income or known yield instment assset: \
f= $S_0$ - I - K $e^{-rT}$ : known income \
f= $S_0$ $e^{-qT}$ - K $e^{-rT}$ : known yield

### Are Futures prices = Forward prices ?
In general, the answer is no, because of daily settlement. But if r is constant over time, it can be proven that Forward prices = Futures prices. \
Also, if the price of the underlying asset is strongly positively correlated with r, Futures prices > Forward prices .

For the rest of the section, we consider both prices to be the same.

### Futures prices of Stock indices

We consider that the index has a known yield q. \
We have the same formula:  $F_0$= $S_0$ $e^{(r-q)T}$.
If $F_0$ decreases in time, this might mean that q is expected to be greater than r over the period.

### Futures prices of Currencies

If $r_f$ is the foreign risk-free rate of interest, then $F_0$= $S_0$ $e^{(r- r_f)T}$.

### Futures prices on Commodities

For commodities, you have to consider storage costs (treated as a negative income). \
Therefore, if the storage costs are independent of the price of the underlying asset $S_0$, we have: $F_0$= ($S_0$ + U) $e^{rT}$ \
If, this time storage costs are proportional to $S_0$,then: $F_0$= $S_0$ $e^{(r+u)T}$.

### Convenience yield

For some commodities such as gold or silver, it might favorable to hold the asset. This advantage is assumed to be a yield, noted y. \
In this case, the Futures prices should take this into consideration. Therefore, $F_0$ $e^{yT}$= ($S_0$ + U) $e^{rT}$

### Cost of carry

You can also want to consider all the fees paid (storage costs and interest) as a single variable c, called cost of carry. In the following table is the value of c depending on each type of asset considered such as $F_0$ = $S_0$ $e^{cT}$

| Asset type                  | Cost of carry \(c\)  |
|-----------------------------|----------------------|
| Non-Dividend-paying stock   |  c = $r$             |
| Stock index                 |  c = $r - q$         |
| Currencies                  |  c = $r - r_f$       |
| Commodity                   |  c = $r - q + u$     |

For a consumption asset: $F_0$ = $S_0$ $e^{(c-y)T}$  where y is the convenience yield


## Sources

John C.~Hull, Options, Futures, and Other Derivatives, 11th Edition, Pearson. \
Ernest P.~Chan, Algorithmic Trading: Winning Strategies and Their Rationale, Wiley Finance. 


