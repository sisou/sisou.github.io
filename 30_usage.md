---
layout: default
title: Usage
nav_order: 30
permalink: /usage
---

# Usage

## Initialization

To start the client, just instantiate the `HubAPI` class by passing it the URL
of the Nimiq Hub to connect to:

```javascript
// Connect to testnet
const hubApi = new HubApi('https://hub.nimiq-testnet.com');

// Connect to mainnet
const hubApi = new HubApi('https://hub.nimiq.com');
```

## Calling Methods

Call an API method on your `HubApi` instance in the context of a user action:

```javascript
document.getElementById('checkoutBtn').addEventListener('click', function(event) {
  // Call the API here:
  hubApi.checkout({ /* options */ });
});
```

By default, the client opens a popup window for user interactions. On mobile
devices, a new tab will be opened instead. For simplicity, we will always refer
to popups throughout this documentation.

Popups will be blocked by browsers if not opened within the context of a user
action. Thus, it is required that API methods are called _synchronously_ within
a user action, such as a click.

For more details about avoiding popup blocking, please refer to
[this article](https://javascript.info/popup-windows#popup-blocking).

## Using Redirects

Please refer to the [Using Redirects](/using-redirects) section.

---

Next: [API Methods](/api-methods)
