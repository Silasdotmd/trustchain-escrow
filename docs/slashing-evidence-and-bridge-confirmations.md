# Slashing evidence and bridge confirmations

Slashing evidence is an on-chain event payload. The governance contract accepts
only non-empty evidence up to 256 bytes, which supports content-addressed
references while keeping event resource use bounded. Invalid evidence returns
`InvalidSlashEvidence` and leaves stake and recipient balances unchanged.

Bridge confirmation reads distinguish three conditions: no record
(`BridgeConfirmationMissing`), a recorded but non-final confirmation
(`BridgeConfirmationPending`), and a stale update attempting to reduce the
stored count (`BridgeConfirmationRegression`). Confirmation counts may only
increase for the same bridge protocol.

Bridge configuration operations remain admin-authorized. The confirmation
update is intentionally permissionless under the contract's existing public
interface; consumers must use the stored finality state, not an unverified
off-chain observation.
