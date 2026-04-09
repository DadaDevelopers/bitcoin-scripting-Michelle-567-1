Given Script
OP_DUP OP_HASH160 <PubKeyHash> OP_EQUALVERIFY OP_CHECKSIG

1. Breakdown of Each Opcode

OP_DUP
Duplicates the top item on the stack
Used to keep a copy of the public key

OP_HASH160
Applies:
SHA-256
then RIPEMD-160
Converts public key → public key hash

<PubKeyHash>
This is the expected hash (from the Bitcoin address)

OP_EQUALVERIFY
Checks:
computed_hash == expected_hash
If false → script fails immediately

OP_CHECKSIG
Verifies:
Signature
Against public key
Confirms the spender owns the private key

3. Identify what happens if signature verification fails
If OP_CHECKSIG fails:

Stack returns FALSE
Script execution stops
Transaction is invalid
Miner will reject it

*No Bitcoin is spent.

4. Explain the security benefits of hash verification
OP_HASH160 + OP_EQUALVERIFY provides:

a) Privacy
Public key is hidden until spending
Prevents early exposure
b) Protection Against Key Attacks
Even if quantum computers improve, hashed keys add protection layer
c) Prevents Wrong Key Usage
Ensures only the correct public key is used
