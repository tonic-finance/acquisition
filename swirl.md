# Tonic 🌀 Swirl

## Dollar Cost Averaging

Dollar-cost averaging is the simplest strategy to build up a position in any tradable assets. It consists of placing a buy order for a set quantity at a predetermined time interval. By doing so, it samples the price as it evolves in time removing human mistakes due to fear or greed.

## Decentralized DCA on Ethereum

Implementing DCA on Ethereum in a decentralized way is prone to high gas costs. In particular, finding the right balance between best execution and transactional overhead can be difficult or impossible with small order sizes. Front running and high availability must also be taken into account.

## Swirl

To solve these issues, we have created Swirl, a Peer to Contract DCA running on Ethereum L1.

### How it works

Swirl works in this way, a user creates an order specifying:

- Time-frequency (Hourly, Daily, Weekly, Monthly)
- Token to sell
- Token to buy
- Amount per period
- Number of executions

‌After approving the contract and depositing the wanted amount in the Swirl vault, the protocol will start executing purchase at the appropriate times on the user's behalf

Under the hood, Swirl consolidates and tracks all users balances and allows incentivised keepers to perform single swaps according to the predefined time and quantity schedule.

Any user can edit or close its account at any time. Purchased tokens can also be withdrawn at any time or automatically when closing an active account.

### Features

#### Anti-frontrunning/Slippage facility

To mitigate slippage due to front running or excessive volatility, Swirl implements a circuit breaker which halts the swap if the quoted swap price is too far from the price provided by a reference price feed. We currently support this feature for any pair with a Chainlink feed.

#### Composability

Swirl is capable of more than merely swapping tokens. Thanks to a pluggable architecture, any pair can have a customized execution strategy.

> For example the pair USDC/crvRenWSBTC is capable of performing the
> following steps in a single execution for all users with great gas
> savings:
>
> 1.  Swap USDC to WBTC
> 2.  Deposit WBTC into Curve
> 3.  Deposit crvRenWSBTC into Badger Sett

#### ‌Internal Matching

Swirl is already set up to support internal matching. Internal matching greatly decreases slippage by matching opposite Swirl pairs at the oracle (or TWAP price) with only the overflowing quantities hitting external AMMs.

#### Custom withdrawals

Swirl allows customization for withdrawal behaviour. For example renBTC can be withdrawn as native BTC to the provided BTC address.

#### Fees

To incentivize execution at the right time, Swirl compensates executors with a fee. The initial fee will be set at 0.1%.

‌There are no fees for deposits or withdrawals.

‌

### Gas Cost

| Operation                                | Gas Cost | Est. with 100gwei @$1500/ETH |
| ---------------------------------------- | -------- | ---------------------------- |
| Account creation/edit for 10 executions  | ~190k    | ~$28.5                       |
| Account creation/edit for 50 executions  | ~330k    | ~$49.5                       |
| Account creation/edit for 100 executions | ~560k    | ~$84                         |
| Account closure                          | ~330k    | ~$49.5                       |
| Withdrawal                               | ~65k     | ~$9.75                       |
| Total Executions Cost (Simple Swap)      | ~250k    | ~$37.5                       |
| Per user execution cost with 50 users    | ~5k      | ~$0.75                       |

### Protocol Components
![](https://user-images.githubusercontent.com/65851681/113667556-e2e0fd80-96a8-11eb-962d-9e0c0deaa5ad.png)
