---
description: Use flexible privacy groups
---

# Using flexible privacy groups

!!! warning

    Orion features have been merged into Tessera!
    Read our [Orion to Tessera migration guide](https://docs.orion.consensys.net/en/latest/Tutorials/Migrating-from-Orion-to-Tessera/)
    and about all the [new Tessera features](https://consensys.net/blog/quorum/tessera-the-privacy-manager-of-choice-for-consensys-quorum-networks).

Use the [`web3js-quorum` library](https://github.com/ConsenSys/web3js-quorum) to create and update
membership of [flexible privacy groups](../../Concepts/Privacy/Flexible-PrivacyGroups.md).

!!! tip

    Because group membership for flexible privacy groups is stored in a smart contract, flexible
    privacy groups are also known as onchain privacy groups.

!!! important
    [Flexible privacy groups](../../Concepts/Privacy/Flexible-PrivacyGroups.md) are an early access
    feature. Do not use in production networks.

    The flexible privacy group interfaces may change between releases. There may not be an
    upgrade path from flexible privacy groups created using v1.5 or earlier to enable use of flexible privacy
    group functionality in future versions.

    We do not recommend creating flexible privacy groups in a chain with existing
    [offchain privacy groups](../../Concepts/Privacy/Privacy-Groups.md).

## Enabling flexible privacy groups

Use the [`--privacy-flexible-groups-enabled`](../../Reference/CLI/CLI-Syntax.md#privacy-flexible-groups-enabled)
command line option to enable [flexible privacy groups](../../Concepts/Privacy/Flexible-PrivacyGroups.md).
When flexible privacy groups are enabled, the [`priv_createPrivacyGroup`](../../Reference/API-Methods.md#priv_createprivacygroup),
[`priv_deletePrivacyGroup`](../../Reference/API-Methods.md#priv_deleteprivacygroup),
and [`priv_findPrivacyGroup`](../../Reference/API-Methods.md#priv_findprivacygroup) methods for
[offchain privacy groups](../../Concepts/Privacy/Privacy-Groups.md) are disabled.

## Simple flexible privacy group example

To create and find a [flexible privacy group](../../Concepts/Privacy/Flexible-PrivacyGroups.md) using
the [`web3js-quorum` library](https://github.com/ConsenSys/web3js-quorum):

1. Update the `example/keys.js` file to match your network configuration.

1. Run:

    ```bash
    cd example/onchainPrivacy
    node simpleExample.js
    ```

    This script creates the flexible privacy group with two members. `findPrivacyGroup` finds and
    displays the created privacy group.

!!! tip

    The Tessera logs for Tessera 1 and Tessera 2 display `PrivacyGroupNotFound` errors. This is
    expected behavior because private transactions check offchain and onchain to find the privacy
    group for a private transaction.

## Adding and removing members

To add and remove members from a [flexible privacy group](../../Concepts/Privacy/Flexible-PrivacyGroups.md),
use the `addTo` and `removeFrom` methods in the [`web3js-quorum` library](https://github.com/ConsenSys/web3js-quorum)
client library.

!!! note

    When adding a member, Besu pushes all existing group transactions to the new member and
    processes them. If there are a large number of existing transactions, adding the member might
    take some time.
