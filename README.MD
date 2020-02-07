This tool lets you generate extended private keys and extended public keys in various 
formats for use with Electrum. It also lets you derive xpubs and child xprvs from parent 
xprvs. It's designed so that you can pipe the output to electrum and directly create 
wallets with it. Run it with `python3 xprv.py -h` to see the options.

It requires electrum 3.3.6 or later installed on your system. It uses electrum functions to 
do it's job.

** ref：
Electrum uses a few different derivation paths for various script types. For example for legacy p2pkh addresses (addresses beginning with 1) it uses m/n/i where m is the extended private key (xprv) derived from the seed, n is 0 for external and 1 for change addresses and i is the address index with addresses being generated sequentially starting from 0. Electrum also lets you create a wallet using any xprv and then it'll assume that xprv is m in the derivation path and generate addresses relative to that. So all you have to do is restore your wallet from a hardened xprv such m/1' and electrum will then generate addresses relative to that. These addresses will not be visible to the person who has the extended public key for m.

To generate a wallet using m/1' you can use this script like so:

electrum getmasterprivate| python3 xprv.py -m - -d "m/1'" -p|electrum -w wallet_name restore -
