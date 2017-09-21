# Glacier
Glacier is a protocol for secure cold storage of bitcoins.
[https://www.glacierprotocol.org](https://www.glacierprotocol.org)


This repository contains a security improvement of Glacier Protocol in exchange for more complex execution and the possibility of forgetting an easy-to-remember passphrase. It's not yet working, just in proof of concept stage, so don't use it!

The improvement contains a passphrase similar to Bitcoin Trezor hardware wallet, but with stronger key derivation function.

This modification makes it hard for a third party that gets an information packet to see the value of the money stored on the multisig address. It still contains a private key that can be used as a founder’s fee. The protocol also makes it harder to retrieve the bitcoins even if all cold storage information packets compromised.

The changes are the following:
An optional passphrase parameter is added to create-deposit-data and create-withdrawal-data subprograms.
If passphrase is given, the generated original private key generated WIF string is transformed with scrypt key derivation function with the private key as password, (private key || passphrase) as salt, and n=2^17, m=100, p=1, dkLen=32 parameters to get the real private key (needed RAM for this is 2.5G), that are transformed to WIF private keys that are used in the transactions. 

For increased security of the passphrase, it's important not to store the passphrase with the original private keys.

Other improvements that need to be made:
- The secret key format is not checked in the input. It MUST be checked to make sure that it was written down correctly. I tried to sign with the first 2 keys and the last 2 keys separately when I was verifying that the secret keys were written down correctly.
