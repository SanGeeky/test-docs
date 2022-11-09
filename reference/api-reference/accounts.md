---
description: >-
  This endpoint returns the necessary to manage an account in Mintacoin: address
  (Mintacoin public key), signature (Mintacoin secret key), and seed words (to
  recover the signature).
---

# 👤 Accounts

## **Create account**

{% swagger baseUrl="https://sandbox.api.mintacoin.co" method="post" path="/accounts" summary="Creates an account on Mintacoin and on the given blockchain" %}
{% swagger-description %}
This endpoint returns the necessary to manage an account in Mintacoin: 

**address**

 (Mintacoin public key), 

**signature**

 (Mintacoin secret key), and 

**seed words**

 (to recover the signature).
{% endswagger-description %}

{% swagger-parameter in="body" name="blockchain" required="false" type="String" %}
The blockchain in which the account's first wallet will be created
{% endswagger-parameter %}

{% swagger-response status="200" description="Account successfully created" %}
```javascript
{
  "data": {
     "address": "D6J2KKOOXSTOXO36REKBPL3QH4FL2PCFKBK6W3TIOVMHR7DDVLTQ",
     "seed_words": "movie enrich merit census grid twice praise return glass wagon yard faint",
     "signature": "DCZIKJFUC6O5R2PVDDPB2C3XFGJL2ZCRKV66WNCPB4UDCP64HQLQ"
  },
  "status": 201
}
```

{% tabs %}
{% tab title="Response data" %}
| Parameter    | Type   | Description                                                                                                 |
| ------------ | ------ | ----------------------------------------------------------------------------------------------------------- |
| `address`    | String | Public key of your Mintacoin account.                                                                       |
| `signature`  | String | Secret key of your Mintacoin account. keep it safe and don't share it.                                      |
| `seed_words` | String | 12 words that you can use to recover your `signature` if you lost it, keep them safe, and don't share them. |
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Permission denied" %}
{% tabs %}
{% tab title="Invalid Token" %}
```json
{
  "code": 401,
  "detail": "Invalid authorization Bearer token",
  "status": "unauthorized"
}
```
{% endtab %}

{% tab title="Missing Token" %}
```json
{
  "code": 401,
  "detail": "Missing authorization Bearer token",
  "status": "unauthorized"
}
```
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

<details>

<summary>Parameters Example</summary>

```json
{
  "blockchain": "stellar"
}
```



</details>

<details>

<summary>CURL Request</summary>

```bash
curl -X POST \
     -H 'Content-Type: application/json' \
     -d '{"blockchain": "stellar"}' \
     "https://sandbox.api.mintacoin.co/accounts
```

</details>

{% hint style="info" %}
Blockchains supported: `:stellar`
{% endhint %}

## **Recover Signature**

{% swagger baseUrl="https://sandbox.api.mintacoin.co" method="post" path="/accounts/:address/recover" summary="Recovers the account signature" %}
{% swagger-description %}
Recover the signature with the 

`address`

 and the 

`seed_words`

 of an account.
{% endswagger-description %}

{% swagger-parameter in="body" name="seed_words" required="true" type="String" %}
Account's seed words
{% endswagger-parameter %}

{% swagger-parameter in="path" name="address" type="String" required="true" %}
Account's address
{% endswagger-parameter %}

{% swagger-response status="200" description="Account's signature sent" %}
```json
{
  "data": {
     "signature": "DCZIKJFUC6O5R2PVDDPB2C3XFGJL2ZCRKV66WNCPB4UDCP64HQLQ"
  },
  "status": 200
}
```

{% tabs %}
{% tab title="Response data" %}
| Parameter   | Type   | Description                           |
| ----------- | ------ | ------------------------------------- |
| `signature` | String | Secret key of your Mintacoin account. |
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

<details>

<summary>Parameters Example</summary>

```json
{
  "seed_words": "movie enrich merit census grid twice praise return glass wagon yard faint"
}
```



</details>

<details>

<summary>CURL Request</summary>

```bash
curl -X POST \
     -H 'Content-Type: application/json' \
     -d '{"seed_words": "movie enrich merit census grid twice praise return glass wagon yard faint"}' \
     "https://sandbox.api.mintacoin.co/accounts/D6J2KKOOXSTOXO36REKBPL3QH4FL2PCFKBK6W3TIOVMHR7DDVLTQ/recover"
```

</details>

## **Create asset trustline**

{% swagger baseUrl="https://sandbox.api.mintacoin.co" method="post" path="/accounts/:address/assets/:asset_id/trust" summary="Create an asset trustline to allow the account to hold an asset" %}
{% swagger-description %}
The resulting response is the information of the asset requested to own.
{% endswagger-description %}

{% swagger-parameter in="body" name="signature" required="true" type="String" %}
Secret key of your Mintacoin account
{% endswagger-parameter %}

{% swagger-parameter in="path" name="address" type="String" required="true" %}
Account's address
{% endswagger-parameter %}

{% swagger-parameter in="path" name="asset_id" required="true" type="String" %}
Asset’s identifier 
{% endswagger-parameter %}

{% swagger-response status="200" description="Asset trustline created" %}
```json
{
  "data": {
    "code": "MTK",
    "id": "317e8c9c-48ad-4513-8936-32646edbed9b",
    "supply": "123.542"
  },
  "status": 201
}
```

{% tabs %}
{% tab title="Response data" %}
| Parameter | Type   | Description                             |
| --------- | ------ | --------------------------------------- |
| `id`      | String | The asset’s id.                         |
| `code`    | String | The asset’s code.                       |
| `supply`  | String | The amount of the asset in the network. |
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

<details>

<summary>Parameters Example</summary>

<pre class="language-json"><code class="lang-json"><strong>{
</strong>  "signature": "PSUQJNRDUZL7KLGB4O5FMN6M7XH3LTOWWU3IPGVKTWU7IBNHAQNQ"
}</code></pre>

</details>

<details>

<summary>CURL Request</summary>

```bash
curl -X POST \
     -H 'Content-Type: application/json' \
     -d '{"signature": "PSUQJNRDUZL7KLGB4O5FMN6M7XH3LTOWWU3IPGVKTWU7IBNHAQNQ"}' \
     "https://sandbox.api.mintacoin.co/accounts/YYVLNUJFEW54QZIHWZTIBLAD52M5TSXOJAZP7FYJXC7TM7MQQDLQ/assets/317e8c9c-48ad-4513-8936-32646edbed9b/trust"
```

</details>

## Get assets balances

{% swagger method="get" path="/accounts/:address/assets" baseUrl="https://sandbox.api.mintacoin.co" summary="Retrieve the assets information held by a Mintacoin ac>count and their balances" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" type="String" name="address" required="true" %}
Account's address
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="List of assets" %}
```json
{
  "data": [
    {
      "asset": "MTK",
      "asset_id": "438d075c-2b66-4841-bf92-2c9f346e16fa",
      "balance": "0.0",
      "blockchain": "stellar",
      "minter": false
    },
    {
      "asset": "NYY",
      "asset_id": "be6bd87e-6956-4f2d-b316-f14ece2ca677",
      "balance": "123.455",
      "blockchain": "stellar",
      "minter": true
    }
  ],
  "status": 200
}
```

{% tabs %}
{% tab title="Response data" %}
| Parameter    | Type    | Description                                                                                                                              |
| ------------ | ------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `asset`      | String  | Asset’s code.                                                                                                                            |
| `asset_id`   | String  | Asset’s id.                                                                                                                              |
| `balance`    | String  | The current balance of the asset on the user's account.                                                                                  |
| `blockchain` | String  | The name of the blockchain to which the asset belongs.                                                                                   |
| `minter`     | Boolean | <p><code>true</code> if the user account is the issuer of the asset.<br><code>false</code> if the user account only holds the asset.</p> |
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

<details>

<summary>CURL Request</summary>

```bash
curl -X GET \
     -H 'Content-Type: application/json' \
     "https://sandbox.api.mintacoin.co/accounts/YYVLNUJFEW54QZIHWZTIBLAD52M5TSXOJAZP7FYJXC7TM7MQQDLQ/assets"
```

</details>
