---
description: >-
  Here it is described some of the basic knowledge to start using the Mintacoin
  API, for example, the base URL and also the structure for the success and
  error responses.
---

# 📔 General Info

## Base URL

Currently, Mintacoin offers a Sandbox URL. Useful for testing and getting started with the API, the transactions are sent to the testnet of the supported blockchains.

```url
https://sandbox.api.mintacoin.co/v1-alpha
```

### Success response

A successful response has the following format:

```json
{
  "data": {
      ...
  },
  "status": 200 | 201
}
```

#### **Response parameters**

| Parameter | Type    | Description                                                  |
| --------- | ------- | ------------------------------------------------------------ |
| `data`    | Object  | Contains the data returned by the endpoint you're accessing. |
| `status`  | Integer | HTTP response status code.                                   |

### Error response

An error response has the following format:&#x20;

```json
{
 "code": "blockchain_not_found",
 "detail": "The introduced blockchain doesn't exist",
 "status": 400
}
```

{% tabs %}
{% tab title="Response parameters" %}
| Parameter | Type    | Description                                                |
| --------- | ------- | ---------------------------------------------------------- |
| `code`    | String  | Result code of the response that communicates the failure. |
| `detail`  | String  | Description of the error response.                         |
| `status`  | Integer | Status code of the response.                               |
{% endtab %}

{% tab title="Standard error responses" %}
<table data-header-hidden><thead><tr><th>Code</th><th>Detail</th><th data-type="number">Status</th></tr></thead><tbody><tr><td><code>asset_not_found</code></td><td>The requested asset doesn't exist.</td><td>400</td></tr><tr><td><code>blockchain_not_found</code></td><td>The introduced blockchain doesn't exist.</td><td>400</td></tr><tr><td><code>decoding_error</code></td><td>Address, signature or seed words are invalid.</td><td>400</td></tr><tr><td><code>encryption_error</code></td><td>Error during encryption.</td><td>400</td></tr><tr><td><code>invalid_address</code></td><td>The address is invalid.</td><td>400</td></tr><tr><td><code>invalid_seed_words</code></td><td>The seed words are invalid.</td><td>400</td></tr><tr><td><code>invalid_address</code></td><td>The address is invalid.</td><td>400</td></tr><tr><td><code>invalid_supply_format</code></td><td>The introduced supply format is invalid. This must be a number greater than zero.</td><td>400</td></tr><tr><td><code>wallet_not_found</code></td><td>The introduced address doesn't exist or doesn't have an associated blockchain.</td><td>400</td></tr><tr><td><pre><code>unauthorized</code></pre></td><td><pre><code>Invalid authorization Bearer token</code></pre></td><td>null</td></tr><tr><td></td><td><pre><code>Missing authorization Bearer token</code></pre></td><td>null</td></tr></tbody></table>
{% endtab %}
{% endtabs %}
