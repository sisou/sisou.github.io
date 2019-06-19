---
name: Quick Start
layout: default
nav_order: 5
---

# Quick Start
{: .no_toc }

Get started in three easy steps:

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Add script

Add this to your HTML page:

<script src="https://cdn.jsdelivr.net/npm/@nimiq/hub-api@v1.0/dist/standalone/HubApi.standalone.umd.js"></script>
```html
<script src="https://cdn.jsdelivr.net/npm/@nimiq/hub-api@v1.0/dist/standalone/HubApi.standalone.umd.js"></script>
```

## Init Hub API

Put this in your script:

<script>
  const hubApi = new HubApi('https://hub.nimiq-testnet.com');
</script>
```javascript
const hubApi = new HubApi('https://hub.nimiq-testnet.com');
```

## Get a user's address

Add a click handler to a button and call a Hub API method:

<div class="code-example">
  <p>Your address: <span id="output">-</span></p>
  <p><button id="choose-address" class="btn btn-primary">Choose Address</button></p>

  <script>
    document.getElementById('choose-address').addEventListener('click', async function(event) {
      const output = document.getElementById('output');

      try {
        const result = await hubApi.chooseAddress({ appName: 'Hub API Docs' });
        output.textContent = result.address;
      } catch (error) {
        output.textContent = error.message;
      }
    });
  </script>
</div>
```html
Your address: <span id="output">-</span>
<button id="choose-address">Choose Address</button>

<script>
  document.getElementById('choose-address').addEventListener('click', async function(event) {
    const output = document.getElementById('output');

    try {
      const result = await hubApi.chooseAddress({ appName: 'Hub API Docs' });
      output.textContent = result.address;
    } catch (error) {
      output.textContent = error.message;
    }
  });
</script>
```

---

For more details about available methods on the `HubApi`, please see the [API Methods](/api-menthods).
