---
title: "Liquidation"
---

# What is Liquidation?
To ensure there is enough collateral in the system to guarantee the value of all outstanding Dai, a CDP can be liquidated if it is deemed unsafe. This occurs when the value of the collateral (as judged by the Oracle) is less than the required collateralization for the asset class. During the liquidation process, a CDP is locked, enough collateral is seized to cover its debt plus fees, and the remaining collateral is then made available to the user.

The Dai Stablecoin System relies on a special a class of users, called Keepers, to identify and close CDPs which have become undercollateralized. The Keepers are charged with maintaining the health of the system by comparing a Risk Parameter called the Liquidation Ratio with the actual Collateral-to-Debt ratio of the CDP.
# Why does it exist?
Unlike most types of fiat, which hold value only by government decree, Dai is a modern and cryptographically secure incarnation of representative currency; all circulating Dai are backed by a surplus of collateral tokens stored in smart contracts, ensuring trustlessness and eliminating counterparty risk. It is this complete transparency that maintains user confidence in the system.

To make sure that the required surplus of collateral exists at all times, a class of users called Keepers are charged with keeping a constant watch for CDPs that become unsafe or under-collateralized. These Keepers are a special category of the Dai Stablecoin System users. They are the actors in the system who are incentivized to make sure that the outstanding Dai supply remains fully collateralized and solvent. They help maintain the health of the entire ecosystem by ensuring that unsafe CDPs are offered up for liquidation as quickly as possible. This is particularly important during rapid market downturns as collateral value could fail to satisfy the debt obligation.
# What is the Liquidation Ratio?
Each collateral type supported by the CDP engine has its own Liquidation Ratio, which is determined based on the risk profile assigned to that particular asset. These profiles are evaluated and then ratified by a decentralized governance process. This combination of risk profile, and the delayed market price as determined by the Oracle Feed, is what defines the Liquidation Ratio.

For example: Bob wants to draw 200 DAI and thinks the value of his collateral will not drop below 50% of its current market price. He therefore decides to stake at least double the minimum collateralization threshold. Since the minimum collateralization is 150%, Bob deposits $600 of ETH and draws 200 DAI, leaving him with a CDP at 300% collateralization.

**It is important to remember that 150% is the lowest point at which a CDP can avoid being liquidated.** All users should stay well above that minimum level in anticipation of normal market volatility. It can be helpful to periodically review the collateralization ratio of the [entire system](https://mkr.tools/) and use that as an indicator of what the community of users at large feels is a secure margin of safety.
# What is the Liquidation Price?
This is the lowest unit price the staked collateral can reach before the CDP becomes vulnerable to liquidation.
# What is the Liquidation Penalty?
This is a fee that is added to the total outstanding DAI debt when a liquidation occurs, which is subtracted from a user's collateral holdings. 

Proceeds from penalty fees are transferred to the PETH pool which increases the ratio of WETH that users receive when they remove their collateral from a CDP. This fee inflates the value of the collateral pool during periods when there are a lot of liquidations, for example due to high level of instability in the market.
# What happens if I get Liquidated?
Liquidation occurs when a Keeper closes a CDP and sends it to the Liquidity Providing Contract (LPC), which in turn, offers the CDPs assets for sale on the Dai Dashboard. Once the debt obligations have been met, the unsold PETH collateral is returned to the CDP owner.

The order of operations looks like this:

*   The defaulted CDP is closed.
*   The Penalty Fee is applied to the DAI debt in addition to the current Stability Fee. (Note that the Stability Fee is set to 0 for Single Collateral Dai)
*   The LPC removes enough PETH collateral to satisfy the debt at current Oracle Prices.
*   The CDP owner is now able to remove their remaining collateral from the closed position.
*   The seized PETH is offered for sale at [dai.makerdao.com](http://dai.makerdao.com) with an incentivising discount, called the Boom/Bust Spread, applied to the value.
*   The DAI earned from the sale of PETH is burned to wipe out the CDP debt.
*   If there is excess DAI from the sale, it is sold for PETH which is returned to the Pool of Ether, inflating its value.
*   If there is insufficient DAI from the sale, then PETH is drawn from the pool and offered for sale to cover the shortfall. This dilutes the total value of the pool.

An auction model will replace the current mechanism when the system transitions to Multi Collateral Dai.
# How much of my collateral will I have left if I get liquidated?
To determine how much collateral you would possess after a liquidation you can use the following simplified formula:

`(Collateral * Oracle Price * PETH/ETH Ratio) - (Liquidation Penalty * Stability Debt) - Stability Debt = (Remaining Collateral * Oracle Price) DAI`

Assuming:

*   The Oracle Price of one ETH is 350USD
*   The total Locked PETH is 10 ETH
*   The ratio of PETH/ETH is 1.012
*   The Liquidation Penalty is 13%
*   The CDP has a Stability Debt of 1000 DAI

`(10 × 350 × 1.012) − (13% × 1000) − 1000 = 2412 DAI or 6.891428571 ETH`
# How do I calculate my Liquidation Price?
You can use the following simplified formula to determine how far the value of your collateral must fall in order to trigger a settlement:

`(Stability Debt * Liquidation Ratio) / (Collateral * PETH/ETH Ratio) = Liquidation Price`

Given that:

*   The value of one ETH is 350USD
*   The total staked PETH is 12
*   The ratio of PETH/ETH is 1.012
*   The Liquidation Ratio is 150%
*   The Stability Debt is 1000 DAI

`(1000 × 1.5 ) ÷ (12 × 1.012) = 123.51 USD`

The price of ETH would need to fall to 123.51 USD to before the CDP is considered unsafe and is at risk of being liquidated. 
# How do I calculate my Collateralization Ratio?
If you would prefer to determine the health of your position by looking at a ratio of collateral to debt, as opposed to a Liquidation Price, you can use the following simplified formula:

`(Locked PETH × ETH Price × PETH/ETH Ratio) ÷ Stability Debt × 100 = Collateralization Ratio`

Given that:

*   The value of one ETH is 350USD
*   The total staked PETH is 12
*   The ratio of PETH/ETH is 1.012
*   The Stability Debt is 1000 DAI

`(12 × 350 × 1.012) ÷ 1000 × 100 = 425.04%`

The CDP has a Collateralization Ratio of 425.04%.
# What is the best way to lower my risk of liquidation?
The primary risk to CDP owners is maintaining a safe leveraged position in a highly unpredictable market. To secure your position, the amount you have borrowed must always be worth significantly less than the amount you have staked. If your CDP is close to the liquidation price, you must either add more collateral or return DAI to reduce that risk.

Which option you choose depends on your long-term goals. If you firmly believe in the future value of your underlying collateral, you may decide to add more to your position. Or, if you would like to lower your exposure to price volatility, you would pay down your debt by returning DAI to your CDP. 

The best way to lower your risk of liquidation is to repay DAI, as your Liquidation Price decreases far more efficiently. This also has the added benefit of reducing the amount of interest you accrue on your position.

Assuming:

*   The value of one ETH is 350USD
*   The total staked PETH is 12
*   The ratio of PETH/ETH is 1.012
*   The Liquidation Ratio is 150%
*   The Stability Debt is 1000 DAI

Current Liquidation Price:

`(1000 × 1.5 ) ÷ (12 × 1.012) = 123.51 USD`

Liquidation Price change by **adding** 700 USD worth of collateral:

`(1000 × 1.5 ) ÷ (**14** × 1.012) = 105.87 USD`

Liquidation Price change by **removing** 700 USD worth of debt:

`(**300** × 1.5 ) ÷ (12 × 1.012) = 37.05 USD`

We can see that the Liquidation Price is significantly reduced by returning DAI as opposed to adding more collateral.
# How does the smart contract sell collateral?
When a Keeper liquidates an unsafe CDP, the Liquidity Providing Contract (LPC) ensures the collateral is offered for sale on the Dai Dashboard. The sale price is determined by the Oracle feeds with a special modifier applied. This modifier generally takes the form of a discount, that is then applied to the outstanding debt that must be recovered. This additional 'spread' is designed to incentivize a quick recapitalization of the system by offering a better than market price to collateral buyers.

Users can purchase PETH that has been seized by the LPC on the dashboard. Any DAI surplus from the sale can be bought with PETH. 
# Can I purchase seized PETH?
On the DAI dashboard, there is a section entitled "Total Liquidity Available from forced CDP liquidations" where market participants can purchase seized PETH at a discount as determined by the Bust/Boom Spread.
# What are the risks to DAI holders if there are a lot of liquidations?
If the system is behaving as it was designed, there should be little or no noticeable impact on DAI price due to the over-collateralization of assets.

If a significant portion of the total CDP owners have failed to maintain the safety of their positions adequately, the system as a whole may become under-collateralized. In this scenario, a Global Settlement might be triggered to ensure that DAI holders can redeem their tokens for the underlying collateral at the settled Target Price.
# Where can I view live information about liquidations?
https://mkr.tools/system/liquidations
# Best Practices to avoid getting liquidated
It is important to remain aware of the health of your CDP as you are its sole owner and are fully responsible for ensuring that your assets remain safe from liquidation. The Dai Stablecoin System is a decentralized set of smart contracts, and there exists no entity that is in charge of operation of the system. It is a very good idea to set price alerts in your favorite app, or in multiple apps, so you are not surprised by market events.

Remember that opening a CDP represents the creation of Risk. How much risk you are willing to take on is dependent on multiple factors. Determining what your [risk profile](https://www.investopedia.com/terms/r/risk-profile.asp) looks like is a science in itself but something everyone should take some time to figure out.

Always ensure you have sufficient liquid assets available that can be used to top up your position, or assets you can sell for DAI to pay down your debt. If you have a significant amount of collateral staked, and you believe the market may be taking a sustained downturn, you can also draw excess collateral from your CDP that you can sell for DAI which you can then use to pay down your debt. **Make very sure that you don't approach your Liquidation Price in the process.**

Struggling to acquire liquidity in a chaotic market can be very stressful. Particularly during events that may cause exchanges to crash, congested networks, or high gas prices. Never allow your CDP to become under-collateralized, you do not want to be stuck on a bus during a market crash.

For further information on risks please refer to [Terms of Service](#find-the-terms) that provide important legal information. Every CDP user needs to accept [Terms of Service](#find-the-terms) prior to using the Dai Stablecoin System.
