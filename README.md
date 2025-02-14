# Cross-Chain-Rebase-Token
1. This project is about to create a cross-chain rebase token using **CCIP**.


## key points
1. A protocol that allows users to deposit into a vault and in return, receive rebase tokens that represent their underlying balance.
2. The rebase token's balance of function is dynamic to show the changing balance with time.
3. The protocol sets an interest rate for each user based on some global interest rate of the protocol at the time the user deposits into the vault.


## Core contracts
1. **RebaseToken**: An ERC-20 token contract with **Ownable** and **AccessControl** for permission management, implementing **yield-bearing token mechanics** through method overrides and extensions, requiring deployment on both source and destination chains.  
2. **Vault**: A treasury contract that allows users to **deposit ETH** to mint corresponding **rebase tokens** with accrued interest and enables redemption by **minting interest first**, then **burning the rebase tokens** to withdraw ETH.  
3. **RebaseTokenPool**: A contract inheriting CCIP’s **TokenPool**, managing a single token while integrating a **router, RMN...**, enabling **burn & mint** or **lock & unlock** mechanisms for cross-chain operations.

## test
1. Use **fork testing** to test the cross-chain-rebase-token on Sepolia and Arbitrum
   1. [Enable tokens in CCIP](https://docs.chain.link/ccip/tutorials/cross-chain-tokens/register-from-eoa-burn-mint-foundry)
2. use script to deploy and test on Sepolia and Avalance Fuji


## steps to bridge all tokens:
1. on Sepolia fork(source chain)：
   1. getNetworkDetails
   2. deploy the `sourceRebaseToken` and `tokenPool`
   3. deploy the `vault`
   4. grant mint-and-burn role to `vault` and `tokenPool`
   5. register `sourceRebaseToken` as Admin in `RegistryModuleOwnerCustom`
   6. make `sourceRebaseToken` accept Admin role in `TokenAdminRgistry`
   7. Link `sourceRebaseToken` to `tokenPool` in the token admin registry
2. on ArbSepolia fork(dest chain)：
   1. getNetworkDetails
   2. deploy the `destRebaseToken` and `tokenPool`
   3. grant mint-and-burn role to `vault` and `tokenPool`
   4. register `destRebaseToken` as Admin in `RegistryModuleOwnerCustom`
   5. make `destRebaseToken` accept Admin role in `TokenAdminRgistry`
   6. Link `destRebaseToken` to `tokenPool` in the token admin registry
3. add a remote pool and token to localPool mutually
4. deposit ETH and receive tokens
5. bridge the tokens by `ccipSend()` and call the destPool to mint
6. validate the result