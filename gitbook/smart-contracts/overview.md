# Summary of Smart Contracts

The following is a general overview of the smart contracts used by White Whale:

- **Pool network**: a coordinated network of LPs (e.g., Atom-Luna; and Atom-Juno) for each supported token on selected 
chains (e.g., Terra and Juno)
- **WW Pool**: each LP in the network of LPs (e.g., Atom-Luna; and Atom-Juno) is primarily accessible by bots and not users.
- **Vault Network**: vaults (e.g. Atom, Luna, and Juno) store tokens needed to make flash loans.
- **Flashloan vaults**: vaults of tokens selected for the Vault Network.
- **Pool Factory and Vault Factory**: each manages the deployment and parameters of WW pools and vaults. Requires governance permission.
- **Fee collector**: contract that collects fees for WW.

Detailed information can be found in each contract's section. 