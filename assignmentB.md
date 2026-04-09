Implement a Hashed Time-Lock Contract for atomic swap between Alice and Bob:
Alice can claim with secret preimage within 21 minutes
Bob gets refund after 21 minutes

1. HTLC Script
OP_IF
    OP_HASH160 <HashOfSecret> OP_EQUALVERIFY
    <AlicePubKey> OP_CHECKSIG
OP_ELSE
    <Timeout> OP_CHECKLOCKTIMEVERIFY OP_DROP
    <BobPubKey> OP_CHECKSIG
OP_ENDIF

<!-- Explanation
 IF branch (Alice claims)
Must provide:
Secret (preimage)
Signature
 ELSE branch (Refund)
After 21 minutes:
Bob can claim refund
Uses time lock -->

2. Claim Script (Alice)
<Signature_Alice> <Secret> OP_TRUE
<!-- OP_TRUE triggers IF branch -->

3. Refund Script (Bob)
<Signature_Bob> OP_FALSE
<!-- OP_FALSE triggers ELSE branch -->

4. Test Values
Secret: supersecret123
Hash160: <your generated hash>
Timeout: block 800006

<!-- Timeout
Bitcoin uses block height or timestamp
Example:
Current block: 800000
Timeout: 800006  (~21 minutes ≈ 6 blocks) -->

<!-- Full Flow 
✔ Alice Claims
Provides:
Secret
Signature
Script checks:
Hash matches 
Signature valid 
Funds released
✔ Bob Refunds
Waits 21 minutes
Provides signature
Time lock passes
Funds returned -->
