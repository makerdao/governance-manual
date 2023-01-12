# Table of Contents

* [Maker Operational Manual](README.md)

## MakerDAO
* Structure
  * [Maker Improvement Proposals](governance/mips.md)
  * [Core Units](core-units/core-units.md)
* Overview
  * [Status and Dashboards](protocol-status/protocol-and-dao-status.md)
  * [Core Unit Budget Flow](core-units/core-unit-budget-flow.md)
  * [Common Abbreviations and Acronyms](protocol-status/acronyms.md)
  * [Discord Servers](misc/discords.md)
* Calendars
  * [MakerDAO Calls Calendar](protocol-status/calls-calendar.md)
  * [MakerDAO Governance Calendar](protocol-status/governance-calendar.md)

## Governance
* Governance Cycle
  * [Monthly Governance Cycle](governance/monthly-governance-cycle.md)
  * [Weekly Governance Cycle](governance/weekly-governance-cycle.md)
* Flowcharts
  * [Governance Flow](governance/governance-flow.md)
  * [Urgent Governance Flow](governance/urgent-governance-flow.md)
  * [Governance Process Selector](governance/governance-process-selection-flow.md)
* [Voting](governance/voting-in-makerdao.md)
  * [Practical Guide to Voting](governance/practical-guide-voting.md)
  * [Gasless Poll Voting](governance/gasless-poll-voting.md)
  * [On-Chain Governance](governance/on-chain-governance.md)
  * [Approval Voting Guide](governance/approval-voting-guide.md)
  * [Video Guide To Voting In The Maker Protocol](governance/how-to-vote.md)
* Verification
  * [Executive Audit](governance/executive-audit.md)
  * [GSM Exceptions](governance/gsm-exceptions.md)
* Off-Chain
  * [Off-Chain Governance](governance/off-chain-governance.md)
  * [Impact Estimations](governance/impact-estimations.md)
  * [Proposal Bounties](governance/proposal-bounties.md)
* Technical MIPs
  * [Best Practices](governance/technical-mips-development-best-practices.md)
  * [Code Example](governance/technical-mip-code-example.md)
* [Emergency Shutdown](governance/emergency-shutdown.md)  
## Delegation
  
* Overview
  * [What is Delegation?](delegation/what-is-delegation.md)
  * [Separation of Powers](delegation/separation-of-powers.md)
  * [Delegate Metric Tracking](delegation/delegate-metric-tracking.md)
* For MKR Holders
  * [MKR Holders Guide to Delegation](delegation/mkr-holder-guide.md)
  * [MKR Holders Agreement](delegation/mkr-holder-agreement.md)
  * [How To Delegate Video](delegation/mkr-holder-how-to-delegate.md)
* For Delegates  
  * [Recognized Delegate Requirements](delegation/recognized-delegate-requirements.md)
  * [Delegates Code of Conduct](delegation/delegates-code.md)
  * [Why Become a Recognized Delegate?](delegation/why-to-become-a-recognized-delegate.md)
  * [How to Attract More MKR as a Recognized Delegate?](delegation/delegate-attract-more-mkr.md)
* [Delegate Contract Migration](delegation/delegate-expiration.md)
  
## Collateral
* [Overview](collateral/collateral-overview.md)
* Real World Assets In Detail
  * [6s Capital](collateral/6s.md)
  * [New Silver DROP](collateral/new-silver.md)
  * [ConsolFreight DROP](collateral/consolfreight.md)
  * [FortunaFi DROP](collateral/fortunafi.md)
  * [Harbour Trade Credit DROP](collateral/harbour-trade.md)
  * [Huntingdon Valley Bank](collateral/hvbank.md)
  
## Parameter Index

* Core
  * [Governance Pause Delay](parameter-index/core/param-gsm-pause-delay.md)
  * [Maximum System Surplus](parameter-index/core/param-system-surplus-buffer.md)
  * [Dai Savings Rate](parameter-index/core/param-dai-savings-rate.md)
  * [Global Liquidation Limit](parameter-index/core/param-global-liquidation-limit.md)
  * [Global Debt Ceiling](parameter-index/core/param-global-debt-ceiling.md)
* Vault Risk
  * [Stability Fee](parameter-index/vault-risk/param-stability-fee.md)
  * [Debt Ceiling](parameter-index/vault-risk/param-debt-ceiling.md)
  * [Liquidation Ratio](parameter-index/vault-risk/param-liquidation-ratio.md)
  * [Liquidation Penalty](parameter-index/vault-risk/param-liquidation-penalty.md)
  * [Debt Floor](parameter-index/vault-risk/param-debt-floor.md)
  * [RWA Agreement](parameter-index/vault-risk/param-rwa-agreement.md)
* Collateral Auction
  * [Auction Price Function](parameter-index/collateral-auction/param-auction-price-function.md)
  * [Auction Price Multiplier](parameter-index/collateral-auction/param-auction-price-multiplier.md)
  * [Local Liquidation Limit](parameter-index/collateral-auction/param-local-liquidation-limit.md)
  * [Max Auction Drawdown](parameter-index/collateral-auction/param-max-auction-drawdown.md)
  * [Max Auction Duration](parameter-index/collateral-auction/param-max-auction-duration.md)
  * [Breaker Price Tolerance](parameter-index/collateral-auction/param-breaker-price-tolerance.md)
  * [Proportional Kick Incentive](parameter-index/collateral-auction/param-proportional-kick-incentive.md)
  * [Flat Kick Incentive](parameter-index/collateral-auction/param-flat-kick-incentive.md)
* Surplus Auction
  * [Surplus Auction Lot Size](parameter-index/surplus-auction/param-surplus-lot-size.md)
  * [Surplus Auction Minimum Bid Increase](parameter-index/surplus-auction/param-min-bid-increase-flap.md)
  * [Surplus Auction Duration](parameter-index/surplus-auction/param-auction-duration-flap.md)
  * [Surplus Auction Bid Duration](parameter-index/surplus-auction/param-bid-duration-flap.md)
  * [Surplus Auction Limit](parameter-index/surplus-auction/param-surplus-auction-limit.md)
* Debt Auction
  * [Debt Auction Minimum Bid Decrease](parameter-index/debt-auction/param-min-bid-decrease-flop.md)
  * [Debt Auction Duration](parameter-index/debt-auction/param-auction-duration-flop.md)
  * [Debt Auction Bid Duration](parameter-index/debt-auction/param-bid-duration-flop.md)
  * [Debt Auction Delay](parameter-index/debt-auction/param-debt-auction-delay.md)
  * [Debt Auction Bid Size](parameter-index/debt-auction/param-bid-size.md)
  * [Debt Auction Initial Lot Size](parameter-index/debt-auction/param-initial-lot-size.md)
  * [Debt Auction Lot Size Increase](parameter-index/debt-auction/param-lot-size-increase.md)


## Module Index
* [Peg Stability](module-index/module-psm.md)
* [Debt Ceiling Instant Access](module-index/module-dciam.md)
* [Token Streaming](module-index/module-token-streaming.md)
* [DAI Direct Deposit](module-index/module-dai-direct-deposit.md)
* [Flash Mint](module-index/module-flash-mint-module.md)
* [Linear Interpolation](module-index/module-lerp.md)
* [Emergency Shutdown](module-index/module-emergency-shutdown.md)
