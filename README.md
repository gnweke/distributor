# merkle-distributor

A program for distributing tokens efficiently via uploading a [Merkle root](https://en.wikipedia.org/wiki/Merkle_tree).

## Install Anchor CLI

This repository targets Anchor 0.31.x and Solana 2.3.x. Install the CLI tools before building:

```bash
cargo install --locked anchor-cli@0.31.1
sh -c "$(curl -sSfL https://release.solana.com/v2.3.0/install)" -- --no-modify-path
```

## Local Dev Quickstart (macOS & Ubuntu)

### Toolchain install

```bash
rustup toolchain install 1.83
cargo install --locked anchor-cli@0.31.1
sh -c "$(curl -sSfL https://release.solana.com/v2.3.0/install)" -- --no-modify-path
npm install -g yarn
```

### Smoke test

```bash
solana-test-validator -r &
sleep 5
solana config set -ul
solana airdrop 2
```

### Build and test

```bash
anchor build -p merkle_distributor
anchor test -p merkle_distributor
```

Troubleshooting: ensure no OpenSSL dependency leaks.

```bash
cargo tree -p merkle-distributor -i openssl-sys
```

## Claiming Airdrop via CLI

To claim via CLI instead of using `https://jito.network/airdrop`, run the following commands.

1. Build the cli (must have rust + cargo installed):

```bash
cargo b -r
```

2. Run `claim` with the proper args. Be sure to replace `<YOUR KEYPAIR>` with the _full path_ of your keypair file. This will transfer tokens from the account `8Xm3tkQH581s3MoRHWUNYA5jKbgPATW4tJAAxgwDC6T6` to a the associated token account owned by your keypair, creating it if it doesn't exist.

```bash
./target/release/cli --rpc-url https://api.mainnet-beta.solana.com --keypair-path <YOUR KEYPAIR> --airdrop-version 0 --mint jtojtomepa8beP8AuQc6eXt5FriJwfFMwQx2v2f9mCL --program-id mERKcfxMC5SqJn4Ld4BUris3WKZZ1ojjWJ3A3J5CKxv claim --merkle-tree-path merkle_tree.json
```

Note that for searchers and validators, not all tokens will be vested until December 7, 2024. You can check the vesting status at `https://jito.network/airdrop`.
