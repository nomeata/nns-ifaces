# Network Nervious System Canister Interfaces

## Introduction

Using the [DFINITY Canister SDK](https://sdk.dfinity.org) `dfx` to call a canister that exists outside of a `dfx` project, such as any of the NNS canisters, can lead to garbled [Candid](https://github.com/dfinity/candid) output. This is because `dfx` does not support this use case, consequently does not ship with these canister interfaces, and therefore does not know how to display results correctly by default. Fortunately, there is a simple workaround. The Candid compiler `didc` allows you to suggest how results should be displayed. This repository contains `.did` files that facilitate the workaround. See the example below.

## Example

Get information about a neuron.

```bash
NETWORK="https://ic0.app" # Mainnet
CANISTER="rrkah-fqaaa-aaaaa-aaaaq-cai" # Governance canister
METHOD="get_neuron_info" # Get neuron info method
ARGUMENTS="(1_553_249_650_525_229_399:nat64)" # Neuron identifier
RESULT="$(dfx canister --no-wallet --network=$NETWORK \
    call $CANISTER $METHOD $ARGUMENTS --output=raw \
)"
didc decode -t "(Result_2)" -d governance.did $RESULT
```
