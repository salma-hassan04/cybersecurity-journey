# Lab 01: GPG Signing

Hands-on Domain 1 (Security+ SY0-701) lab: digital signatures in practice.

## Goal

Understand digital signatures by doing them — sign a file with my private key, verify it with the public key, and watch verification fail the moment the file changes. Built to fix a weak spot from my Domain 1 quiz: what actually gets signed, and why a signature proves who sent something.

## Setup

- Ubuntu on WSL, GnuPG 2.4.4
- One lab folder (`gpg-lab`); GPG keeps the keys itself in its `~/.gnupg` keyring
- No existing keys — everything generated fresh for this lab

## What I did

1. Generated a key pair with `gpg --gen-key` — entered a name, email, and passphrase; got a public and secret key, a fingerprint, an expiry date (3 years), and a ready-made revocation certificate
2. Created `message.txt` (26 bytes) and signed it with `gpg --detach-sign` → produced a separate 119-byte `message.txt.sig`; the original file was untouched and still readable
3. Signed a much bigger file (~270 KB) → the signature was still exactly 119 bytes, proving the signature is made from a fixed-size fingerprint of the file, not the file itself
4. Verified with `gpg --verify message.txt.sig` → "Good signature from Salma", no passphrase needed, because verifying uses only the public key
5. Changed one character in `message.txt` with nano and verified again → "BAD signature". Changed it back → Good again. The signature was never broken; the file just stopped matching it
6. Exported my public key with `gpg --armor --export > mykey.pub` — a plain-text block safe to send to anyone

## What I learned

When I signed the file, the computer took a fingerprint of it and sealed that fingerprint in a way only my key can do. Checking the signature means taking a fresh fingerprint of the file and comparing it with the one sealed at signing time. When I changed one letter, the fresh fingerprint no longer matched the sealed one, so the check failed instantly.

A stranger can't fix the seal to match their edited file, because making a new seal needs my private key, and that never leaves my machine. The other half of the pair — the public key — can only check seals, never make them, which is why I can hand it to anyone.

The part that surprised me: anyone with my public key can open the seal. That's the design, not a flaw — what's inside is only the fingerprint of the message, nothing secret. Signing was never about hiding anything. The security is that nobody except me could have made a seal that checks out. That's why a computer trusts a download or a signed message from someone it has never met.

## What I'd do differently

- Do the lab in the morning instead of the evening — more focus
- Learn the editor basics (nano save/exit) before a lab so they don't interrupt the flow
- Check `--help` with grep (`gpg --help | grep -i armor`) earlier instead of scrolling the whole manual
