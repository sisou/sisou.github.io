---
title: Checkout
layout: default
parent: API Methods
nav_order: 10
---

# Checkout

The `checkout()` method allows your site to request a transaction from the user.
This will open a popup for the user to select the address to send from &mdash;
or cancel the request. During the payment process, the signed transaction is
sent (relayed) to the network but also returned to the caller, e.g. for
processing in your site, storage on your server or re-submittal.

## Request

```javascript
const requestOptions = {
    // The name of your app, should be as short as possible.
    appName: 'Nimiq Shop',

    // [optional] The path to an image on the same origin as the request is sent
    // from, must be square and will be displayed with up to 146px width and hight.
    shopLogoUrl: 'https://your.domain.com/path/to/an/image.jpg',

    // The human-readable address of the recipient (your shop/app).
    recipient: 'NQ07 0000 0000 0000 0000 0000 0000 0000 0000',

    // [optional] Nimiq.Account.Type of the recipient.
    // Only required if the recipient is a vesting (1) or HTLC (2) contract.
    // Default: Nimiq.Account.Type.BASIC (0)
    //recipientType: Nimiq.Account.Type.HTLC,

    // Value of the transaction, in luna.
    value: 100 * 1e5, // 100 NIM

    // [optional] Transaction fee in luna.
    // Default: 0
    //fee: 138,

    // [optional] Extra data that should be sent with the transaction.
    // Type: string | Uint8Array | Nimiq.SerialBuffer
    // Default: new Uint8Array(0)
    //extraData: 'Hello Nimiq!',

    // [optional] Human-readable address of the sender.
    // If the address exists in the user's Hub, this parameter
    // forwards the user directly to the transaction-signing after the
    // balance check.
    // Default: undefined
    //sender: 'NQ07 0000 0000 0000 0000 0000 0000 0000 0000',

    // [optional] Whether to force the submitted sender address
    // If this parameter is true, an exception is thrown when either the
    // submitted sender address does not exist or does not have sufficient
    // balance. When false, the user will be shown the address selector
    // for the above conditions instead.
    // (Only relevant in connection with the `sender` parameter)
    // Default: false
    //forceSender: true,

    // [optional] Nimiq.Transaction.Flag, only required if the transaction
    // creates a contract.
    // Default: Nimiq.Transaction.Flag.NONE (0)
    //flags: Nimiq.Transaction.Flag.CONTRACT_CREATION,

    // [optional] The duration (in number of blocks) that the signed transaction
    // should be valid for. The maximum is 120.
    // Default: 120
    //validityDuration?: number;
};

// All client requests are async and return a promise
const signedTransaction = await hubApi.checkout(requestOptions);
```

## Result

The `checkout()` method returns a promise which resolves to a `SignedTransaction`:

```javascript
interface SignedTransaction {
    serializedTx: string;                  // HEX signed and serialized transaction
    hash: string;                          // HEX transaction hash

    raw: {
        signerPublicKey: Uint8Array;       // Serialized public key of the signer
        signature: Uint8Array;             // Serialized signature of the signer

        sender: string;                    // Human-readable address of sender
        senderType: Nimiq.Account.Type;    // 0, 1, 2 - see recipientType above

        recipient: string;                 // Human-readable address of recipient
        recipientType: Nimiq.Account.Type; // 0, 1, 2 - see above

        value: number;
        fee: number;
        validityStartHeight: number;       // Automatically determined validity
                                           // start height of the transaction
        extraData: Uint8Array;
        flags: number;
        networkId: number;
    }
}
```

The `serializedTx` can be handed to a Nimiq JSON-RPC's `sendRawTransaction` method.
The `raw` object can be handed to the NanoApi's `relayTransaction` method.
