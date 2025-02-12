# Cross-Chain-Rebase-Token
1. This project is about to create a cross-chain rebase token using **CCIP**.


## key points
1. A protocol that allows users to deposit into a vault and in return, receive rebase tokens that represent their underlying balance.
2. The rebase token's balance of function is dynamic to show the changing balance with time.
3. The protocol sets an interest rate for each user based on some global interest rate of the protocol at the time the user deposits into the vault.


## test
1. Use **fork testing** to test the cross-chain-rebase-token on Sepolia and Arbitrum
   1. [Enable tokens in CCIP](https://docs.chain.link/ccip/tutorials/cross-chain-tokens/register-from-eoa-burn-mint-foundry)
2. use script to deploy and test on Sepolia and Avalance Fuji

