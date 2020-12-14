# Swap Basis Curve

The term structure of an interest rate basis curve is defined as the relationship between the basis zero rate and it’s maturity. Basis curves are used as the forecast curves for pricing interest rate products. The increase in basis spreads has resulted in large impacts on non-standard instruments.

The increase in basis spreads or basis zero rate spread has resulted in large impact on pricing non-standard instruments. Basis curve acts as forecast curve in model input for valuing financial products. Hence, basis spread curves are required for getting accurate pricing,

Typical basis curves are 1 month, 6 months, 12 months, Prime, FedFun, and OIS. A 1-month basis curve is displayed below. Note that the market quote of a basis swap rate is the spread over the associated 3 month reference rate.

he term structure of a basis curve is constructed from a set of market quotes of some liquid market instruments. Normally a basis curve is divided into two parts. The short end of the term structure is determined using LIBOR rates. The remaining is derived using basis swaps.

The objective of the bootstrap algorithm is to find the zero yield or discount factor for each maturity point and cash flow date sequentially so that all basis curve instruments can be priced back to the market quotes. All bootstrapping methods build up the term structure from shorter maturities to longer ones. The output of the construction process is the zero rate curves of basis indices, such as 1-month, 6-month, or 12-month.

The basis swap valuation model can be found at basis swap model.

First you need to construct the base yield curve as guided at yield curve construction.

Assuming that we have had all the yields of a 6-month swap curve data up to 4 years and now need to derive up to 5 years.

Let x be the yield at 5 years.
Use an interpolation method to get yields at 4.5 years as Ax
Given the 5 year basis swap spread, we can use a root-finding algorithm to solve the x that makes the value of the 5 year inception basis swap equal to zero.
Now we obtain all yields or equivalent discount factors up to 5 years
Repeat the above procedure till the longest basis swap maturity.

There are two keys in yield curve construction: interpolation and optimization for root finding.

Most popular interpolation algorithms in curve bootstrapping are linear, log-linear and cubic spline. They can be applied to either zero rates or discount factors.

Some critics argue that some of those simple interpolations cannot generate smooth forward rates and the others may be able to produce smooth forward rates but fail to match the market quotes. Also they cannot guarantee the continuity and positivity of forward rates.

The monotone convex interpolation is more rigorous. It meets the following essential criteria:

Replicate the quotes of all input underlying instruments.
Guarantee the positivity of the implied forward rates
Produce smooth forward curves.

Although the monotone convex interpolation rule sounds almost perfectly, it is not very popular with market practitioners.

As described above, the bootstrapping process needs to solve a yield using a root finding algorithm. In other words, it needs an optimization solution to match the prices of curve-generated instruments to their market quotes.

FinPricing employs the Levenberg-Marquardt algorithm for root finding, which is very common in curve construction. Another popular algorithm is the Excel Solver, especially in Excel application.

You can find more details at

https://finpricing.com/lib/IrCurveIntroduction.html
