# Doex-Core
DOEX trading smart contracts enabling long and short positions for call and put tokenized, collateralized, cash settable european style options.



A dynamic approach was implemented for ensuring collateral for writing options, making use of favorable writer's open option positions for decreasing total required balance provided as collateral.

The exchange accepts stablecoin deposits as collateral for issuing ERC20 option tokens. Chainlink based price feeds provide the exchange onchain underlying price and volatility updates.

Upon maturity each each option contract is liquidated and cash settled by the credit provider contract, becoming open for redemption by token holders. In case any option writer happens to be short on funds during settlement the credit provider will register a debt and cover payment obligations, essentially performing a lending operation.

Registered debt will accrue interest until it's repaid by the borrower. Payment occurs either implicitly when any of the borrower's open option positions matures and is cash settled (pending debt will be discounted from profits) or explicitly if the borrower makes a new stablecoin deposit in the exchange.

Exchange's balances not allocated as collateral can be withdrawn by respective owners in the form of stablecoins. If there aren't enough stablecoins available at the moment of the request due to operational reasons the solicitant will receive ERC20 credit tokens issued by the credit provider instead. These credit tokens are a promise of future payment, serving as a proxy for stablecoins since they can be redeemed for stablecoins at a 1:1 value conversion ratio, and are essential for keeping the exchange afloat during episodes of high withdrawal demand.

Holders of credit tokens can request to withdraw (and burn) their balance for stablecoins as long as there are sufficient funds available in the exchange to process the operation, otherwise the withdraw request will be FIFO-queued while the exchange gathers funds, accruing interest until it's finally processed to compensate for the delay.

Test cases defined in test/finance provide more insight into the implementation progress.
