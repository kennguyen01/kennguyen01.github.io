---
title: Portfolio Allocation and Rebalance Calculator
date: 2020-01-08
categories: programming
---

Every month, I hop on to Vanguard to take a look at my IRA account. Since I don't have automatic investing set up, I manually contribute to my IRA and allocate the money to the specific ETFs that I own. The contribution limit for 2019 was \$6,000 so every month I would contribute $500. While manual contribution seems like additional work compared to using a target date fund, it offers me the advantage of freely allocating my portfolio. The tradeoff is that I need to spend around ten minutes every month crunching the numbers for the allocation. To make the process less tedious, I wrote a simple portfolio rebalance calculator for that. In this post, I'll talk about the rationale behind choosing to do my own allocation and how the rebalance calculator helped me.

Link to Project: [Rebalance Calculator](https://kingle.pythonanywhere.com/rebalance)

<!--more-->

## Manual Allocation Rationale

If there's one thing I learned about investing, it's diversification. By diversifying my portfolio, I lower the risk of losing money when a particular industry is underperforming. Diversification is simply not putting all my eggs in one basket.

### Target Date Funds

With Vanguard, there's a few ways I can do this. The simplest is the [Vanguard Target Retirement Funds](https://investor.vanguard.com/mutual-funds/target-retirement/#/mini/overview/1487). I select how many years I am away from retirement and Vanguard recommends a target date fund that fits my risk profile. For example, if I have 35 years before retirement, my allocation should be:

| <strong>Asset</strong> | <strong>Allocation</strong> |
|------------------------|-----------------------------|
| U.S. Stocks            | 54%                         |
| International Stocks   | 36%                         |
| U.S. Bonds             | 7%                          |
| International Bonds    | 3%                          |

As I become older, Vanguard automatically adjusts my portfolio to be more conservative. That means reducing my allocation in stocks and increases that in bonds. If I am to retire today at 65, my allocation will be:

| <strong>Asset</strong> | <strong>Allocation</strong> |
|------------------------|-----------------------------|
| U.S. Stocks            | 30%                         |
| International Stocks   | 20%                         |
| U.S. Bonds             | 29%                         |
| International Bonds    | 12%                         |
| Short-Term TIPS        | 7%                          |

Target date funds are very common because they allow people to regularly contribute without having to worry about diversification. This comes at a cost, the fees for these funds are typically 0.15%. They are a bit higher than other Vanguard mutual funds and ETFs but not significant enough over the long run. However, the biggest disadvantage for me is that these funds generalize my risk profile.

Planning for retirement can be a complicated topic. To be honest, I don't even know how things will turn out five years from now, much less 35. I might have saved up a good nest egg by the time I'm 65 and retire comfortably. But it's also possible that I might be working long past 65 and need additional money to sustain myself. If there's a market downturn, I'd prefer to shift my portfolio toward more bonds than just 50%.

### Mutual Funds and ETFs

On the other hand, Vanguard also offers mutual funds and ETFs that cover different market categories. Personally I love index mutual funds because I don't want to deal with the volatility of specific stocks. Many popular Vanguard mutual funds also have equivalent ETFs. In general, they are very similar and offer almost the same returns.

I have ETFs in my portfolio because when I first started contributing to my IRA, I did not have the minimum $3,000 investment to start. ETFs do not have such minimums, I only need enough money to purchase one share. I went with four ETFs that covered both domestic and international markets.

| <strong>ETF</strong> | <strong>Allocation</strong> | <strong>Fees</strong> |
|----------------------|-----------------------------|-----------------------|
| U.S. Stock           | 60%                         | 0.03%                 |
| International Stocks | 30%                         | 0.09%                 |
| U.S. Bonds           | 5%                          | 0.035%                |
| International Bonds  | 5%                          | 0.09%                 |

My strategy for investing favors simplicity. I'm only going to buy and hold. I also won't have to deal with taxes with rebalancing because I will be doing it inside my IRA. As my situation changes, I have the freedom to adjust my portfolio accordingly instead of having someone else does it for me.

## Rebalance Calculator

Of course sitting down and crunching the numbers every month is not a task I look forward to. That's why I wrote a simple rebalance calculator to help me with that.

The app takes in a string of tickers, get their names, equity type, and prices from Yahoo Finance. Then I can enter how much I plan to contribute to my IRA, along with my current holding for each ticker and target allocation. Then it calculates how much I need to buy or sell for each ticker to achieve the desired allocation. By letting the computer calculates the number for me, I avoid doing the error prone tedious calculations.
