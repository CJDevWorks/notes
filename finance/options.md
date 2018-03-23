Options
==============

**Terms**

- underlying asset
- strike price
- expiry period
- premium
- current price
- BreakEven
- Buyer and Seller
- Intrinsic Value
- Extrinsic Value (Time Value)
- ATM, OTM, ITM


Call Option and Put Option :
===========================
    - Buyer and Seller
Eg: RealState house Call option()buying a house:

Call option buyer :
- Has the right to buy underlying (real state)at 
strike price (agrred price - 1m) during the expiry period(aggredd period - 3 month) 
after paying premium (20 K)

Call option Seller :
- Has the obligation to sell underlying (real state)at 
strike price (agrred price - 1m) during the expiry period(aggredd period - 3 month) 
and he receives premium (20 K). Premium is not returned whatever is the outcome.

- If the strike price and current price are same its ATM.
- if the strike is higher OTM
- if the strike is less than ITM

            ATM         OTM         ITM

Intrinsic   0           0           200(example strike price :800)

Extrinsic   25          25          25

Why would any one be a Seller :
    - Limited profit (premium) and unlimited lossed(theoretically)
    - Buyer limited loss and unlimited profit.
Then Why to Sell ??

- Sell OTM option probability is higher - less premium but more chances

- Burden of price movement
- Break-even is otm
- Time decay
- Probability is on seller side (due to price buffer)

-- Covered call stretegy
 
Why to be a buyer of ITM option?


Parameters for Options Pricing:
================================


Volatility:
============

standard deviation from mean

what will happen after transaction volatility go up/down ()

Difference between stock volatility and options volatility?

Historical volatility
Implied volatility based on demand and supply in market

- Implied volatility is a measurement used in the Black-Scholes Model, used to calculate option prices.
- Volatility measures the magnitude of a potential price change in an underlying.
- High Implied Volatility = Stock Price is Less Stable, increases extrinsic value of option prices across the board.
- Low Implied Volatility = Stock Price is More Stable, decreases extrinsic value of option prices across the board.
- Implied volatility rank (IVR) allows you to put context around current implied volatility levels.
dough takes the lowest IV & highest IV level over a specified timeframe and ranks current IV against that range to determine IV rank.


VIX Index:
===========

- Market volatility based on S&M 500
- SPY=>(1/10 ==> S&M)
- High VIX => High Volatility

Options Greeks:
================

Understand individual impact and then collective impact :

**Delta**

 If the underlying price is moved by one dollar value then whats the impact on option/portfolio pnl :

What is DV01 ?
- Rate of change of price (first of price)
call (0-1) =>
(1-0.5) => ITM 
(0.5) => ATM 
(0.5-0) => ATM

Gama :

Vega :

Theta :

rho :

"Moneyness" of an option : Where is the money wrt strike price (ATM,OTM, ITM)

**GAMMA**


**VEGA**


**THETA**

Time Decay :
     - Is same for Call and put
     - increases exponential
