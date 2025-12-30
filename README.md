# Crypto_Staking_Governance_Protocol
Overview

A modular, upgradeable ETH staking platform with:

dETH — deposit-wrapped ETH.

sETH — staking reward token.

StakingPool — UUPS upgradeable staking logic with proportional reward distribution.

RewardController — manages reward token distribution.

Dashboard — read-only staker analytics.

GovernanceToken — ERC20 snapshot token for governance and voting.

Contracts
1. dETH.sol

ETH wrapper ERC20.

deposit(), withdraw(amount).

ERC20-compatible: transfer, approve, transferFrom, balanceOf.

Events: ETHDeposited, ETHWithdrawn, Approval, Transfer.

2. sETH.sol

Reward ERC20 token for staking.

Minted/distributed via RewardController → StakingPool.

3. StakingPool.sol

Upgradeable (UUPS pattern).

Proportional rewards based on shares.

Key functions:

stake(amount), unstake(sharesToRemove).

claimRewards(), pendingRewards(user).

Roles:

ADMIN_ROLE — manages pool config.

UPGRADER_ROLE — authorizes upgrades.

Events: Staked, Unstaked, RewardClaimed.

4. RewardController.sol

Holds and distributes sETH rewards.

Transfers to pool as needed to fund claims.

5. Dashboard.sol

Analytics contract for frontends.

Functions:

getLeaderboard(count)

getPaginatedStakersDetailed(offset, limit)

getStakerDetails(address)

getStakingActivity(daysAgo)

getStakingOverview()

Integrates with dETH and sETH.

6. GovernanceToken.sol

ERC20 snapshot token for governance.

Functions:

_snapshot() — creates new snapshot.

balanceOfAt(account, snapshotId)

totalSupplyAt(snapshotId)

Useful for voting, dividends, or weighted reward systems.

Security & Best Practices

UUPS upgradeable pattern with restricted _authorizeUpgrade().

SafeERC20Upgradeable for all token transfers.

Reward transfers capped by available sETH in RewardController.

Dashboard analytics are read-only.

Governance snapshots should be admin-restricted to avoid gas attacks.

Deployment & ABI Integration

Each Solidity contract has a compiled JSON ABI
