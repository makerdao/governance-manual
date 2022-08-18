# Governance Attacks

This document does not discuss [Oracle attacks](https://docs.makerdao.com/smart-contract-modules/oracle-module/oracle-security-module-osm-detailed-documentation).

Since Maker is almost entirely controlled by executive spells, a malicious [executive spell](https://manual.makerdao.com/governance/voting-in-makerdao/on-chain-governance#executive-votes) is the natural way to attack the protocol. The simplest attack is to transfer ownership of the protocol from the [Pause Proxy](https://docs.makerdao.com/smart-contract-modules/governance-module/pause-detailed-documentation) to an attacker controlled address.

## How to profit

One way to profit from an attack is to set up trading positions that should benefit from Maker's downfall. For example, it might be possible to create a large short position in the MKR token or go long DAI volatility. Perhaps Maker credit default swaps are available on a prediction market. Anyhow, once these positions are set up then a successful attack on the protocol should result in profit. However, these types of trading positions may be difficult to set up in practice. The simplest way to profit is to confiscate all on-chain bearer assets locked within the protocol. In addition, the attacker could mint a quadrillion DAI and exchange DAI for more bearer assets on lending markets like Aave, Compound, Uniswap, etc.

## Without an Emergency Shutdown Module

There are layers of defenses against such an attack:
- MKR holders would have to approve the spell. This is unlikely to happen because at least some voters should [audit the spell](https://manual.makerdao.com/governance/verification/executive-audit) before voting, and raise the alarm.
- Alternately, the attacker could gather enough MKR together to overcome the vote of honest MKR holders. This would be expensive, but if the cost was not a concern, possible.
- If a malicious spell was approved then the pause timer is started. MKR holders still have a chance to rally votes and cancel the spell before expiration of the [GSM Pause Delay](https://manual.makerdao.com/parameter-index/core/param-gsm-pause-delay).

These may seem like adequate safeguards, but suppose:
- The market capitalization of the MKR token is small compared to the market value of the assets locked in the protocol. A successful attack might profit a million dollars per unit MKR.
- The attack is conducted via a [TakerDAO](https://twitter.com/ameensol/status/1229848488621428736)-like smart contract that allows many individual MKR holders to trustlessly collude.
- The attackers collude with insiders, including Protocol Engineering, GovAlpha, and TechOps. No alarm is raised because the people usually watching for attackers decide to abet the attack.
- Somehow the attackers have a solid plan to dodge legal liability.

This attack is even economically rational. Ethics or altruism is the only thing standing in the way.

## With an Emergency Shutdown Module

With the [Emergency Shutdown Module](https://manual.makerdao.com/module-index/module-emergency-shutdown) (ESM), a minority of MKR holders can shut down the protocol and prevent locked bearer assets from being stolen. However, this process would require swift action and deft coordination.

- MKR exceeding the ESM Threshold must be deposited in the ESM. To underline the gravity of this procedure, MKR deposited into the ESM is burnt.
- Delegates cannot participate in this action because only the underlying MKR holders can deposit to the ESM.
- The ESM Threshold must be exceeded before expiration of the GSM Pause Delay.
- Once successfully shutdown, re-launching the Maker protocol will take considerable political will and delicate consensus building.

Designers of the ESM envisioned that a Maker defense team re-launch the protocol. A new MKR distribution would need to be specified that re-issues the MKR burnt in triggering ESM and burns the MKR used to launch the attack. It may not be feasible to burn all of the attacking MKR because some of it may have already been sold or transferred during the attack. In any case, if this new MKR token, and associated Maker re-deployment, was accepted by the community, this new MKR distribution would great substantial profits to non-attacking MKR.

The ESM adds an economic reason to defend the protocol. Defense is no longer just a matter of altruism, defenders could benefit handsomely from an attack. The ESM flips the economic incentives. Instead of attackers being economically incentivized, attackers can expect no economic benefit due to the economic incentive attached to defending the protocol.
