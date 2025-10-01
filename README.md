# Drop snapshots

This repo is a registry of the THARWA drop allocations for all seasons. 

## Allocation rules

Eligible addresses are those who held one of the tokens: 
- [`0x76972F054aB43829064d31fF5f3AcC5Fabe57FE8`](https://etherscan.io/address/0x76972F054aB43829064d31fF5f3AcC5Fabe57FE8), thUsd. 
- [`0xF88dE5987a4a114Fab1Fe98E681f83216F4b6E76`](https://etherscan.io/address/0xF88dE5987a4a114Fab1Fe98E681f83216F4b6E76), thUsd:USDC curve LP. 

between blocks: 
- start block: [22745986](https://etherscan.io/block/22745986) , right before `thUsd` was deployed.
- end block: [23479244](https://etherscan.io/block/23479244), `2025-01-01 00:00:11 UTC`, end of Season 01

Holding LP curve tokens yields higher allocation than ThUsd. The APY multipliers as follows (see next section for detail description of the calculations):
- `0x76972F054aB43829064d31fF5f3AcC5Fabe57FE8`: APY of 20%
- `0xF88dE5987a4a114Fab1Fe98E681f83216F4b6E76`: APY of 30%

## Detail calculations

The snapshot calculations are as follows:
- Take the balance held over a certain duration gives you points (`blance[wei] * duration[seconds]`)
- These are annualized (calculate the balance that would yield the same value if held for a year), 
- Apply an APY factor on the annualized value, which defines the usd value an account gets.
- Then the usd value is converted to THARWA token using THARWA usd price at the snapshot time.

The allocations from different tokens stack up. If an account holds both thUsd and curve LP balances, he will receive the corresponding amount from each.

### Example calculations for THARWA allocation

User A holds 2,500 thUsd for 45 days.
- Annualized balance is 2500$ * 45 days / 365 days = 308$
- Apply APY factor (20% for thUsd): 308 * 0.2 = 61.64$
- Convert that to tharwa using the snapshot price (0.0085 for example) = 61.64$ / 0.0085 $/THARWA = **7252.21 THARWA**

## Notes

From this snapshot, certain addresses have been excluded:
- Addresses related to Tharwa, like treasury, Tharwa deployer address, etc
- Contract addresses that can't claim their allocations: CurveFi, ThUsdSwap, Tharwa Bonds, wThUsd, etc. 
- Allocations smaller than 10^-15 usd