KMCD - MKR Multi-Collateral Dai (MCD) KSpecification
====================================================

**UNDER CONSTRUCTION**

Useful Links
------------

-   Initial RFP for security audits: <https://www.notion.so/MCD-Security-Audit-ac578a595ac74958877106c77f1b85b0>
-   K-DSS bytecode verification: <https://dapp.ci/k-dss/>
-   DSS solidity sources: <https://github.com/makerdao/dss>
-   Useful invariants: <https://hackmd.io/lWCjLs9NSiORaEzaWRJdsQ> (maybe work `take` is out of date)
-   MCD Documentation: <https://www.notion.so/MCD-Documentation-WIP-2ec33e10c4704243b1c473ec44f42576>
-   MCD Wiki: <https://github.com/makerdao/dss/wiki/Actions>

Structure
---------

-   [mkr-mcd-data](mkr-mcd-data.md) specifies basic data-structures used in the semantics.
-   [mkr-mcd](mkr-mcd.md) specifies the semantics of Vat, which is the core accounting system for MCD.

Potential Properties
--------------------

-   After executing method X of contract C, the suffix of the log will contain these events ...
-   Every time a `ward` changes, a log event should be emmitted which says so (and the log event should have the correct data).
    Will only apply to methods which have `note` modifier, but perhaps should be always.
-   Fundamental equation of Dai (invariant over CDPs + dai).
-   What happens if the "maintenance" functions like `drip` are not called for too long of a timeframe?
    Drip is called by `jug.sol` and `pot.sol`, and if not called frequently enough, system could act funny.

One of the architecture decisions made was to make `*Like` interfaces for actually accessing functions/data of the underlying implementations.
For example, `Cat` has `Urn` defined just to have access to the getters/setters from other contracts.

For inverting storage of `vat` so that we have some implicit account (`msg.sender`), we should inspect `frob` as a test-case, because it access `wish` on three different passed in addresses.

Order to Model
--------------

-   vat.sol
-   lib.sol

Second layer:

-   jug.sol
-   pot.sol
-   spot.sol

Collateral:

-   dai.sol
-   join.sol

Auctions:

-   vow.sol
-   cat.sol
-   flop.sol
-   flip.sol
-   flap.sol

Global:

-   end.sol
