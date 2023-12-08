
![Logo](https://pbs.twimg.com/profile_banners/1627863072772694016/1677531055/1500x500)


# 🔓 Bunkr | Fully On-Chain 2FA [v1 is deprecated -> link to [v2](https://github.com/Bunkr-2FA/bunkr-program/tree/webauthn) ]

Bunkr enables asset protection on Solana by utilizing the widely known TOTP (**T**ime-based **O**ne**T**ime **P**assword) 2FA standard that can be found [here](https://en.wikipedia.org/wiki/Time-based_one-time_password). 

It is compatible with all major Authentication Apps and is frequently used in web2 as a means to secure account access

## ❌ Problem
Wallet security is still lacking inside web2 and on Solana. 

Yes, Ledgers and Multi-Sigs exist, but these options are sub-optimal. One is expensive and the other is hard to understand if you're a new user coming from web2.
## 🏁 Goal / Solution
Provide users on Solana with an option to protect their assets with 2FA that's similar to how they're used to in Web2. Addionally the whole thing should be free, permissionless, trustless, open-source and generally deliver a common good to the Solana ecosystem.

## 🤝 Why Solana?
Quite simple. UX and feasibility. In order to enable web2 style TOTP 2FA, transactions need to:

- be virtually free to the user
- take less than 30s to finality (validity period of an OTP)

Solana nails both of these. Period. 

## 🔒 Security 
 Bunkr as a whole relies on the following security mechanisms to enable asset protection

 - User Private Key (**Baseline**)
 - User chosen password (**Hashchain**)
 - TOTPs (**Merkle Tree**)

## ✔️ How does the OTP mechanism work?

Fundamentally the on-chain OTP Verification is facilitated by a combination of merkle inclusion proofs and Solana's ability to expose a clock/timestamp function at runtime.

Essentially OTPs for any given secret are generated for 6 months upfront, hashed individually, then extended with their timestamp and then hashed again to then represent the leaves of a merkle tree. The root of that merkle tree is then stored on-chain.

 In order to prove the validity of any given OTP the client then just needs to submit the current hashed OTP together with it's corresponding proof path. The on-chain program then extends that hashed OTP with the current on-chain timestamp and simply checks whether that extended hash + the proof path lead to the stored root.

## 🌳 Storage of the Merkle Tree
Surely you're now wondering:

 *"Well, how am I meant to use standard auth apps if I have to store this merkle tree to submit proof paths??"*

And you're totally right. The storage of the tree is a non-trivial task. Not only does the tree need to be readily accessible to the user, but it also needs to not be public and openly crackable. 

**Solution:** The leaves of the tree are stored encrypted on [ShadowDrive](https://docs.genesysgo.com/shadow/shadow-drive). The encryption key is derived from a message the user signs when logging into their Bunkr. That way:

- The user doesn't need to store an extra password
- An attacker needs to have access to the users private key to even start an attempt at cracking the OTP codes.

## 🔒 A rough, but full explanation of the security spec can be found [here](https://gist.github.com/iceomatic/fccf555972f21dbede259fd152343a8a)
 
In the meantime, if you'd like to take a look at any of the transactions, the early version of the Bunkr program is deployed on mainnet at: 
```
BunKrGBXdGxyTLjvE44eQXDuKY7TyHZfPu9bj2Ugk5j2
```
