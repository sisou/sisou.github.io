---
layout: default
title: API Methods
nav_order: 20
has_children: true
permalink: /api-methods
---

# API Methods

## Initialization

To start the client, just instantiate the `HubAPI` class by passing it the URL
of the Nimiq Hub to connect to:

```javascript
// Connect to testnet
const hubApi = new HubApi('https://hub.nimiq-testnet.com');

// Connect to mainnet
const hubApi = new HubApi('https://hub.nimiq.com');
```

## Usage

By default, the client opens a popup window for user interactions. On mobile
devices, a new tab will be opened instead. For simplicity, we will always refer
to popups throughout this documentation.

Popups will be blocked by browsers if not opened within the context of a user
action. Thus, it is required that API methods are called _synchronously_ within
a user action, such as a click:

```javascript
document.getElementById('checkoutBtn').addEventListener('click', function(event){
    hubApi.checkout({ /* options */ });
});
```

For more details about avoiding popup blocking, please refer to
[this article](https://javascript.info/popup-windows#popup-blocking).
