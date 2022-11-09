---
description: Mintacoin will help you in the creation and management of your assets.
---

# 👛 Assets

{% hint style="info" %}
**Definition:** Is the representation of an asset within a blockchain network, which could contain a commercial and economic value; This asset can be exchanged by any other, and it can represent anything like:

> 📍 **Assets examples**
>
> CUP - Coffee Cup
>
> MTK - Mintacoin Token
>
> USDC - Dollar
{% endhint %}

## **Create asset**

{% swagger baseUrl="https://sandbox.api.mintacoin.co" method="post" path="/assets" summary="Creates an asset on the given blockchain" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="blockchain" required="false" type="String" %}
The blockchain in which the asset will be created. Default value: 

`stellar`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" type="String" required="true" %}
The public key of your Mintacoin account. This account will be the owner of the asset
{% endswagger-parameter %}

{% swagger-parameter in="body" name="signature" required="true" type="String" %}
Secret key of your Mintacoin account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="asset_code" required="true" type="String" %}
The asset's identifying code. This code must be alphanumeric and between 1 and 10 characters long
{% endswagger-parameter %}

{% swagger-parameter in="body" name="supply" type="Number" required="true" %}
The initial amount of the asset. This supply must be greater than zero
{% endswagger-parameter %}

{% swagger-response status="200" description="Asset created" %}
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
| `id`      | String | Asset’s id.                             |
| `code`    | String | Asset’s code.                           |
| `supply`  | String | The amount of the asset in the network. |
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

<details>

<summary>Parameters Example</summary>

```json
{
  "blockchain": "stellar", 
  "address": "YYVLNUJFEW54QZIHWZTIBLAD52M5TSXOJAZP7FYJXC7TM7MQQDLQ", 
  "signature": "PSUQJNRDUZL7KLGB4O5FMN6M7XH3LTOWWU3IPGVKTWU7IBNHAQNQ",
  "asset_code": "MTK", 
  "supply": 123.542
}
```



</details>

<details>

<summary>CURL Request</summary>

```bash
curl -X POST \
     -H 'Content-Type: application/json' \
     -d '{"blockchain": "stellar", "address": "YYVLNUJFEW54QZIHWZTIBLAD52M5TSXOJAZP7FYJXC7TM7MQQDLQ", "signature": "PSUQJNRDUZL7KLGB4O5FMN6M7XH3LTOWWU3IPGVKTWU7IBNHAQNQ", "asset_code": "MTK", "supply": 123.542}' \
     "https://sandbox.api.mintacoin.co/assets"
```

</details>

{% hint style="info" %}
Blockchains supported: `:stellar`
{% endhint %}

## Get asset

{% swagger method="get" path="/assets/:id" baseUrl="https://sandbox.api.mintacoin.co" summary="Retrieve the asset information by its asset id" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" type="String" name="id" required="true" %}
Asset’s id
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Asset found" %}
```json
{
  "data": {
    "code": "MTK",
    "id": "317e8c9c-48ad-4513-8936-32646edbed9b",
    "supply": "123.542"
  },
  "status": 200
}
```

{% tabs %}
{% tab title="Response data" %}
| Parameter | Type   | Description                             |
| --------- | ------ | --------------------------------------- |
| `id`      | String | The asset’s identifying id.             |
| `code`    | String | The asset’s identifying code.           |
| `supply`  | String | The amount of the asset in the network. |
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

<details>

<summary>CURL Request</summary>

```bash
curl -X GET \
     -H 'Content-Type: application/json' \
     "https://sandbox.api.mintacoin.co/assets/317e8c9c-48ad-4513-8936-32646edbed9b"
```

</details>

## Get asset issuer

{% swagger method="get" path="/assets/:id/issuer" baseUrl="https://sandbox.api.mintacoin.co" summary="Retrieve the address from the asset's issuer" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" type="String" name="id" required="true" %}
Asset’s id
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Asset issuer sent" %}
```json
{
  "data": {
    "address": "YYVLNUJFEW54QZIHWZTIBLAD52M5TSXOJAZP7FYJXC7TM7MQQDLQ"
  },
  "status": 200
}
```

{% tabs %}
{% tab title="Response data" %}
| Parameter | Type   | Description                         |
| --------- | ------ | ----------------------------------- |
| `address` | String | The public key of the asset issuer. |
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

<details>

<summary>CURL Request</summary>

```bash
curl -X GET \
     -H 'Content-Type: application/json' \
     "https://sandbox.api.mintacoin.co/assets/317e8c9c-48ad-4513-8936-32646edbed9b/issuer"
```

</details>

## Get asset holders

{% swagger method="get" path="/assets/:id/accounts" baseUrl="https://sandbox.api.mintacoin.co" summary="Retrieve the address from the asset's issuer" %}
{% swagger-description %}
The resulting accounts are the holders of the requested asset.
{% endswagger-description %}

{% swagger-parameter in="path" type="String" name="id" required="true" %}
Asset’s id
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Asset issuer sent" %}
```json
{
  "data": {
    "addresses": [
      "6GZTYIJSBPLTKOH3IXTPJNOR6FUQ3ANOF7G6EF3C2ADKQHTNJASA",
      "YYVLNUJFEW54QZIHWZTIBLAD52M5TSXOJAZP7FYJXC7TM7MQQDLQ"
    ]
  },
  "status": 200
}
```

{% tabs %}
{% tab title="Response data" %}
| Parameter   | Type  | Description                                  |
| ----------- | ----- | -------------------------------------------- |
| `addresses` | Array | List of addresses associated with the asset. |
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

<details>

<summary>CURL Request</summary>

```bash
curl -X GET \
     -H 'Content-Type: application/json' \
     "https://sandbox.api.mintacoin.co/assets/317e8c9c-48ad-4513-8936-32646edbed9b/accounts"
```

</details>
