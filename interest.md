---
path: "/interest"
---

# Do the MakerDAO smart contracts collect interest on opened CPDs?

Yes. Maker collects interest called a Governance Fee. It is currently set to 0.5% APR and is calculated against the total amount of Dai drawn on your CDP.

The Governance Fee is calculated _continuously_. As we show in the formulas below, this type of compounding refers to a form of interest that is measured in tiny increments instead of weeks, months, or years. This produces an interest fee that is very close to what one would expect from an annualized compounding.

Let's look at the various results from applying different types of compounding interest, given a debt of 100,000 Dai that has been held for 365 days.

Calculated with annual compounding the future interest fee is:

`100,000 × (1 + (0.5% / 1)) ^ (1 × 1) - 100,000 = 500 DAI`

Calculated with monthly compounding the future interest fee is:

`100,000 × (1 + (0.5% / 12)) ^  (12 × 1)  - 100,000 = 501.14 DAI`

Calculated with continuous compounding the future interest fee is:

`100,000 × 2.7183 ^ (0.5% × 1) - 100,000 = 501.25 DAI`

The difference between annual and continuous compounding interest on a 100,000 Dai debt works out to about **1.25 Dai**.

This format was chosen due to highly variable lifetime of CDPs. As there are no minimum restrictions on how long a CDP has to remain open, it is important for the system to effectively track extremely small accruals.

# What does the system do with the collected fees?

Once the fees have been collected, the smart contract platform transfers the MKR to a contract called the [Burner](https://etherscan.io/token/0x9f8f72aa9304c8b593d555f12ef6589cc3a579a2). As no one has the ability to remove funds from that address, all MKR that is contained there is forever removed from circulation.

# Where can I see my current interest fees?

The outstanding balance owed on a CDP is shown in the Governance Debt column on the Dai Dashboard.

# When do I have to pay interest?

When you pay down your debt by returning Dai to your CDP. You will be charged outstanding interest *proportional to the amount of Dai being returned*. The fee is payable in MKR tokens. In this context, the MKR is required to use a feature of the system, and thus behaves as a utility token.

It's important to ensure you have enough MKR in your wallet to cover the interest charges or the transaction will fail.

# How is it calculated?

## A Simple Example

Given that:

*   A CDP exists with a Stability Debt of **1000** **DAI**
*   The CDP has been open for **30** **days**
*   The current value of a MKR token is **100** **DAI**
*   The Governance Fee is **0.5%**
*   A user pays back a debt of **50** **DAI**

The total Dai denominated cost for paying back **50 DAI** on a **1000 DAI** debt that is **30 days** old is **0.020500948 DAI**, or approximately 2 cents USD.

When the Dai denominated debt is converted to MKR for payment, the total required to complete the transaction is **0.000205009 MKR**.

## A Detailed Example

The total interest accrued in the CDP can be calculated like this:

> (((Total Stability Debt in DAI * (1 + Current Governance Fee in decimal format)) ^ (Age of Stability Debt in days/365)) - Total Stability Debt in DAI ) = Total Governance Debt owed in DAI

When we plug in the values we've already used above we see the interest in DAI owing:

`(1000 * (1 + 0.005) ^ (30÷365)) - 1000 = 0.410018954 DAI`

Now that we have the total interest in Dai, we can convert that to MKR. Assuming an exchange rate where 1 MKR is worth 100 DAI:

`0.410958904 ÷ 100 = 0.004109589 MKR`

And, as the user is repaying 50 DAI, they will be expected to pay the interest accrued on that amount:

`(50 * (1 + 0.005) ^ (30÷365)) - 50 = 0.020500948 DAI`

Now converted to MKR:

`0.020500948 ÷ 100 = 0.000205009 MKR`

The user will need **0.000205009 MKR** in their wallet to cover the accrued interest on **50 DAI** after **30 days**.

After the transaction has been completed, the total amount of interest remaining in the CDP will be:

0.004109589 - 0.000205009 = **0.00390458 MKR**
