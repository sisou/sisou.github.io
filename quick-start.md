---
name: Quick Start
layout: default
nav_order: 5
---

# Quick Start

Get started in three easy steps:

<div class="code-example">
  <p>Your address: <span id="output">-</span></p>
  <button id="choose-address" class="btn btn-primary mb-1">Choose Address</button>

  <script src="https://cdn.jsdelivr.net/npm/@nimiq/hub-api@v1.0/dist/standalone/HubApi.standalone.umd.js"></script>
  <script>
    const hubApi = new HubApi('https://hub.nimiq-testnet.com');

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

<!-- 1. Include the Hub API from a CDN -->
<script src="https://cdn.jsdelivr.net/npm/@nimiq/hub-api@v1.0/dist/standalone/HubApi.standalone.umd.js"></script>
<script>
  // 2. Initialize the Hub API for the testnet (for mainnet use 'https://hub.nimiq.com')
  const hubApi = new HubApi('https://hub.nimiq-testnet.com');

  // 3. Add a click handler to start a Hub API request
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
