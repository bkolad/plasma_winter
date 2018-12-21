# Plasma Winter: governed by SNARKs

This work is a demonstration of applying zk-SNARKs to solving blockchain scalability as a Layer 2 Plasma-like solution.

The code is meant to serve as a Proof-of-concept only and is not suitable for use in production apps. Work on the production-grade implementation is currently in progress. If you want to contribute, please contact the authors:

- Alex Vlasov <alex.m.vlasov@gmail.com> (https://thematter.io)
- Alex Gluchowski <alex@gluchowski.net>

## Spec

https://hackmd.io/cY-VP7SDTUGgPOzDiEU3TQ

## How to run

- Generate a proving key
```
   cargo run --release --bin read_write_keys.rs
```

It will generate a `VerificationKeys.sol` and proving key `pk.key` in a root folder.

- Copy `VerificationKeys.sol` into the `./contracts/contracts/` with replacement

- Replace a `EMPTY_TREE_ROOT` with value `0x09d809ed651bf1f19906bd7c170e1736176d3fbb2053e702dbbc2a8eed3e929f`. It's a root hash of demo server with pregenerated 1000 accounts

- Run the migration by making a proper adjustments in `deploy_example.sh` file

- Run server:
   - Change `start_demo_example.sh` by inserting proper URLs, addresses and keys
   - Run the script

- Server has 1000 accounts pregenerated and you can send using 
```
   POST http://127.0.0.1:8080/send

{
   "from": 0,
   "to": 1,
   "amount": 1000
}
```
- Valid response is 
```
{
   "accepted": true
}
```

- Batch size is 32 transactions, so you need to send this number of txes to start block commitment and proof generation process

- UI lives here `https://github.com/gluk64/gluk64.github.io`, you need to change 
```
   const APIserver = 'https://1be52733.ngrok.io/send'
```

To something else

# License

Plasma Winter is licensed under a
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License.
