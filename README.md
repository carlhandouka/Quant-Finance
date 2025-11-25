# Personal Projects

Python projects in quantitative finance, including portfolio optimization, algorithmic trading, and ML-based market modeling.

The implemented trading strategies remain simple and clear. I implementred them based on books I cite in the sources' section in the end of this document

## Hedging using Forwards and Futures

Hedging using Futures and Forward contracts are based on a simple idea: Take a position in a derivative that offsets the price risk in the underlying asset

### The logic of hedging
A hedge is designed to lock in a future price.

1. Long Hedge (protect against price increases): Use when you plan to buy the asset later.
 One should then take a long position in futures/forwards today.

 2. Short Hedge (protect againzst price decreases): Use when you plan to sell the asset later.
 One should then take a short position in futures/forwards today.

### Ratio of Hedging
1. If the asset you plan to sell/buy is the same the asset on which the Futures/Forward contracts on lying on, the hedge ratio is equal to 1. This is a perfect hedge because this way you can hedge your entire exposure.

2. If this is not case:  Cross-Hedging
We look for Minimum Variance Hedge Ratio: Assumption: $\Delta S = a + b \Delta F + \eps$ (where $\Delta S$ and $\Delta F$ are the variations of prices of the spot and futures prices)
If h is the hedge ratio:   $\Delta S - h \Delta F= a + (b-h) \Delta F + \eps$
Minimum Variance is obtained when $h^{*}$=b. Here b is the slope of the Linear Regression of $\Delta S$ versus $\Delta F$ 



## Pricing Forwards and Futures prices


## Sources

John C.~Hull, Options, Futures, and Other Derivatives, 11th Edition, Pearson.
Ernest P.~Chan, Algorithmic Trading: Winning Strategies and Their Rationale, Wiley Finance.

