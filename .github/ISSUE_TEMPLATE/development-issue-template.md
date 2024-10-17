---
name: Development Issue Template
about: Use this template to file issues you encounter while working on your challenges.
title: "RSA Signature Verification Failure in olehblog Project"
labels: "bug, cryptography, noir"
assignees: ""
---

## Issue Description

Encountering a "Failed to solve program: 'Failed to solve brillig function'" error when running the email signature verification test in the olehblog project. 

## Project Context

**Project Name:** Oleh's zkemail implementation https://github.com/olehmisar/zkemail/tree/main

**Challenge:** ZKEmail Guardian

**GitHub Repository:** (https://github.com/rajeshb62/ab2/tree/main)

## Environment

**Aztec Version:** [Not applicable]

**Noir Version:** >=0.35.0

**Operating System:** macOS

## Steps to Reproduce

1. Navigate to the `zkemail.nr/examples/olehblog` directory
2. Run `nargo test`

## Expected Behavior

The test `test_email` should pass successfully, verifying the email signature.

## Actual Behavior

1. A warning is displayed about the `RevealStringPart` struct never being constructed (may not be relevant).
2. The test `test_email` fails with the error: "Failed to solve program: 'Failed to solve brillig function'"
3. The error trace points to an assertion in the BigNum library used by noir_rsa.

## Code Snippet

```
/ In src/main.nr
pub fn assert_verify_email_signature<let HeadersLen: u32, let BodyLen: u32>(
headers: [u8; HeadersLen],
body: [u8; BodyLen],
pubkey_limbs: [Field; PUBKEY_LIMBS_LEN],
pubkey_redc_limbs: [Field; PUBKEY_LIMBS_LEN],
signature_limbs: [Field; SIGNATURE_LIMBS_LEN]
) {
// ... (implementation details)
assert(rsa.verify_sha256_pkcs1v15(pubkey, headers_hash, signature, 3), "invalid email signature");
}
#[test]
fn test_email() {
// ... (test implementation)
assert_verify_email_signature(
headers,
body,
pubkey_limbs,
pubkey_redc_limbs,
signature_limbs
)
}
```

## Error Messages

```
[olehblog] Running 1 test function
[olehblog] Testing test_email... FAIL
Failed to solve program: 'Failed to solve brillig function'
error: Failed to solve program: 'Failed to solve brillig function'
┌─ /Users/rajeshbhat/nargo/github.com/noir-lang/noir-bignumv0.3.6/src/runtime_bignum.nr:1271:28
│
1271 │ assert(x[i].limbs[j].lt(modulus2[j]));
│ -----------------------------
│
= Call stack:
1. src/main.nr:54:5
2. src/main.nr:37:16
/Users/rajeshbhat/crypto/aztec/wallet_alphabuild/alpha_build2/ab2/email_based_account/noir_rsa/lib/src/rsa.nr:63:33
/Users/rajeshbhat/nargo/github.com/noir-lang/noir-bignumv0.3.6/src/runtime_bignum.nr:739:9
/Users/rajeshbhat/nargo/github.com/noir-lang/noir-bignumv0.3.6/src/runtime_bignum.nr:417:13
/Users/rajeshbhat/nargo/github.com/noir-lang/noir-bignumv0.3.6/src/runtime_bignum.nr:1397:28
/Users/rajeshbhat/nargo/github.com/noir-lang/noir-bignumv0.3.6/src/runtime_bignum.nr:1306:31
/Users/rajeshbhat/nargo/github.com/noir-lang/noir-bignumv0.3.6/src/runtime_bignum.nr:1271:28
```

## Additional Context

**Add any other context about the problem here. This could include:**
1. The error occurs in the BigNum library used by noir_rsa, specifically in an assertion checking the relationship between limbs and a modulus.
2. There's an unused struct `RevealStringPart` in `src/reveal_string.nr` (relevant?).
3. The project uses several dependencies including `zkemail`, `noir_rsa`, `noir_base64`, and `string_search`.

## Possible Solution

**If you have any ideas on how to solve this, please share them here:**

## Impact on Development

This error is preventing the successful testing and verification of email signatures, which is a core functionality of the ZKEmail Guardian project. It blocks further development and testing of the email verification process.


## Support Needed

Guidance on debugging Noir programs, particularly those involving complex cryptographic operations like RSA.
2. Assistance in verifying that the input data (public key, signature, etc.) is in the correct format and size for the RSA verification function.
3. Possible review of the BigNum library implementation to ensure it's compatible with the current version of Noir and the specific RSA parameters being used.
4. Advice on optimizing the code to work within the constraints of the Noir language and its cryptographic libraries.
