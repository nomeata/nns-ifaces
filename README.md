# Network Nervious System Canister Interfaces

## Introduction

Using `dfx`, the [DFINITY Canister SDK](https://sdk.dfinity.org), to call a canister that exists outside of your `dfx` project, such as any of the NNS canisters, can lead to garbled [Candid](https://github.com/dfinity/candid) output. This is because `dfx` does not yet ship with these canister interfaces in scope, and therefore does not know how to display results correctly. It's is a lot like tying to display a Protobuf wire message without the `.proto` file. Fortunately, the Candid `didc` compiler allows you to suggest how results should be displayed. This repository contains `.did` files that facilitate the workaround.

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
