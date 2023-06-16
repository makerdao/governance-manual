# Executive Proxies


## What is an executive proxy?

An executive proxy is a smart contract that sits between the Maker Protocol executive spell and a ‘ProxySpell’ smart contract that triggers a set of actions meant to update or configure an external-to-maker set of smart contracts, such as Spark Protocol.

Unlike the PauseProxy, an executive proxy is not granted any permissions over the core contracts of the Maker Protocol. Instead, it is granted permissions over an external protocol, like Spark.

A key detail of this implementation is that the executive proxy cannot take any action unless it is triggered through a Maker Core executive spell (which can only be done when it is voted to the ‘hat’ by MKR holders).


## What are the benefits of using an executive proxy?

There are two primary benefits to using an executive proxy, rather than interfacing with an external protocol directly using a Maker Core executive spell.

**Security**

The first major benefit is that the contents of a ProxySpell contract cannot affect any of the Maker Core contracts or parameters (in the absence of a heretofore undiscovered bug or exploit within Maker Core.)

Instead, the impact is limited to what access or funding Maker Core governance has given the external protocol over the Core Maker Protocol.

Using Spark as an example, the Spark executive proxy would be able to access DAI up to the debt ceiling granted through the Spark D3M, but no more than that. 

Essentially, the proxy system puts an upper limit on the damage to Maker Core from malicious or bugged code meant to deal with configuration changes in an external set of smart contracts. 

**Process**

Because a ProxySpell can have no impact on Maker Core, it can be created and deployed separately from a Maker Core executive spell.

The process of ProxySpell creation can then be managed by one or more external teams of smart contract developers, improving efficiency by parallelizing spell work.

Further, this also allows the process to prepare a ProxySpell to diverge from the Maker Core executive process if this is deemed worthwhile by the responsible teams. 

Ultimately, this gives the MakerDAO executive process scalability in a way that has not previously been present. 


## How will executive proxies be used in Endgame?

The future plans for executive proxies are that each SubDAO has its own SubDAO Proxy and that this proxy is granted permissions over anything relevant to the given subDAO. 

SubDAOs will be responsible for producing their own ProxySpells if they need changes to be made to contracts or protocols under their control.

SubDAOs will also control the polling process that governs their ProxySpells, with items included in ProxySpells only after SubDAO token holders vote to take action. 

In this paradigm, execution of a SubDAO’s ProxySpell in a MakerCore executive will likely be determined by some combination of Governance Facilitators for Maker Core and the Facilitators managing the SubDAO’s governance processes.