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

## Pricing Forwards and Futures prices


## Sources

John C.~Hull, Options, Futures, and Other Derivatives, 11th Edition, Pearson. \
Ernest P.~Chan, Algorithmic Trading: Winning Strategies and Their Rationale, Wiley Finance. 


