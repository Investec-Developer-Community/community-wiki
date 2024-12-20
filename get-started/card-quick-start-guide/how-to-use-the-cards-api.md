# 💳 How to use the programmable card API

The **Programmable Card API** allows Investec clients to access programmable card functionality via an API. The features available via the online IDE are also available via the API. &#x20;

## **Using Postman**&#x20;

If you’re new to APIs and want to get familiar with using the endpoints, we recommend you create a Postman account (it's free) and use the Postman collections provided to test things out.

{% hint style="info" %}
[**Investec Programmable Banking Postman Collection**](https://www.postman.com/investec-open-api/programmable-banking/overview)
{% endhint %}

Once you’ve signed up for an account, head over to these collections and make sure you **fork the Programmable Card API collection.**

Before querying the API, ensure that you have authenticated: [How to authenticate against the Investec AP](../api-quick-start-guide/how-to-authenticate.md)I

### 1. Get your cards with Postman

_This will return all the cards associated with your account._&#x20;

1. Navigate to the **Card** folder and the **GET Cards query.**&#x20;
2. Hit **Send** to make a call to the API endpoint.

```
https://openapi.investec.com/za/v1/cards
```

3. Take note of the **cardkey** value that is returned. When deploying custom code to your card, you will need to use this variable.&#x20;

<details>

<summary><span data-gb-custom-inline data-tag="emoji" data-code="1f4b3">💳</span> GET Cards example response</summary>

```json
{
   "data": {
       "cards": [
           {
               "CardKey": "1234567",
               "CardNumber": "123456XXXXXX1234",
               "IsProgrammable": true,
               "Status": "Active",
               "CardTypeCode": "VBC",
               "AccountNumber": "11111111111",
               "AccountId": "1111111111222222222233333",
               "EmbossedName": "T TEST"
           },
       ]
   },
   "links": {
       "self": null
   },
   "meta": {
       "totalPages": 1
   }
}
```

</details>

### 2. Update function code on your card with Postman

_This will **save** code your card without publishing it._&#x20;

1. Navigate to the **Card** folder and the **POST Update Function code query.**&#x20;
2. Insert your **cardkey** variable from the previous query under the Params tab on the query page.&#x20;
3. Replace the body of the request with the code you would like. Below is an example for you to use. The snippet declines a card purchases that are made in bakeries (using a specified merchant code) transactions and that are over the R50 (or 5000 cents) limit.&#x20;

{% code overflow="wrap" %}
````json
```
{
    "code": "const beforeTransaction = async (authorization) => { if (authorization.merchant.category.key === 'bakeries') { return authorization.centsAmount < 5000 } return true}"
}
```
````
{% endcode %}

4. Hit **Send** to make a call to the API endpoint.

<pre><code><strong>https://openapi.investec.com/za/v1/cards/:cardkey/code
</strong></code></pre>

5. The **codeID** returned from the response is uniquely generated every time you post/save code to your card, which you will need for your next API call.

<details>

<summary>↪️ Update Function Code example response</summary>

```json
{
   "data": {
       "result": {
           "codeId": "d11bd10e-7cba-1f11-a111-c11e11a1e111",
           "code": "const beforeTransaction = async (authorization) => { if (authorization.merchant.category.key === 'bakeries') { return authorization.centsAmount < 5000 } return true}",
           "createdAt": "2023-04-05T09:33:11.925Z",
           "updatedAt": "2023-04-05T09:33:11.925Z",
           "publishedAt": "2023-04-05T09:33:11.925Z",
           "error": null
       }
   },
   "links": {
       "self": null
   },
   "meta": {
       "totalPages": 1
   }
}
```

</details>

### 3. Publish code to your card using Postman&#x20;

_This will **publish and activate** the code you have saved to your card._&#x20;

1. Navigate to the **Card** folder and the **POST Publish Saved Code query.**&#x20;
2. Insert your **cardkey** variable from the previous query under the Params tab on the query page.&#x20;
3. Replace the body of the code with the following as seen below. Make sure you use the **codeID** from your previous query.&#x20;

<pre class="language-json"><code class="lang-json">{
<strong>   "codeid": "d11bd10e-7cba-1f11-a111-c11e11a1e111",
</strong>   "code": ""
}
</code></pre>

4. Hit **Send** to make a call to the API

<pre><code><strong>https://openapi.investec.com/za/v1/cards/:cardkey/publish
</strong></code></pre>

<details>

<summary><span data-gb-custom-inline data-tag="emoji" data-code="1f468-1f4bb">👨‍💻</span> Publish Saved Code example response</summary>

```json
{
    "data": {
        "result": {
            "codeId": "d11bd10e-7cba-1f11-a111-c11e11a1e111",
            "code": "const beforeTransaction = async (authorization) => { if (authorization.merchant.category.key === 'bakeries') { return authorization.centsAmount < 5000 } return true}",
            "createdAt": "2023-04-05T12:36:43.209Z",
            "updatedAt": "2023-04-05T12:36:43.209Z",
            "publishedAt": "2023-04-05T12:36:56.272Z",
            "error": null
        }
    },
    "links": {
        "self": null
    },
    "meta": {
        "totalPages": 1
    }
}
```

</details>

### 4. Simulate a transaction using Postman&#x20;

_This will run a simulation of your code for testing before you publish code._

1. Navigate to he **Card** folder and the **POST Execute Function Code query.**&#x20;
2. Insert your **cardkey** variable from the previous query under the Params tab on the query page.&#x20;
3. Replace the body of the code with the code you want to simulate. The below code snippet simulates and declines a card purchases that are made in bakeries (using a specified merchant code) transactions and that are over the R50 (or 5000 cents) limit.

```json
{
    "simulationcode": "const beforeTransaction = async (authorization) => { if (authorization.merchant.category.key === 'bakeries') { return authorization.centsAmount < 5000 } return true }",
    "centsAmount": "5050",
    "currencyCode": "zar",
    "merchantCode": 5462,
    "merchantName": "The Coders Bakery",
    "merchantCity": "Cape Town",
    "countryCode": "ZA"
}
```

4. Hit **Send** to make a call to the API

```
https://openapi.investec.com/za/v1/cards/:cardkey/code/execute
```

<details>

<summary><span data-gb-custom-inline data-tag="emoji" data-code="1f911">🤑</span> Simulate a transaction example response</summary>



</details>

### cURL code snippets

#### Get cards

```
curl --location 'https://openapi.investec.com/za/v1/cards' \
--header 'Accept: application/json'
```

#### Update function code

```
curl --location 'https://openapi.investec.com/za/v1/cards//code' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data '{
    "code": "// This function runs during the card transaction authorization flow.\n// It has a limited execution time, so keep any code short-running.\nconst beforeTransaction = async (authorization) => {\n    console.log(authorization);\n    return true;\n};\n\n// This function runs after a transaction.\nconst afterTransaction = async (transaction) => {\n    console.log(transaction)\n};\n\n// This function runs after a transaction.\nconst afterDecline = async (transaction) => {\n    console.log(transaction)\n};"
}'
```

#### Publish code

```
curl --location 'https://openapi.investec.com/za/v1/cards//publish' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data '{
    "codeid": "2d73122b-8beb-4faa-8256-0228ec811f72",
    "code": " "
}'
```

#### Simulate a transaction&#x20;

```
curl --location 'https://openapi.investec.com/za/v1/cards//code/execute' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data '{
    "simulationcode": "// This function runs during the card transaction authorization flow.\n// It has a limited execution time, so keep any code short-running.\nconst beforeTransaction = async (authorization) => {\n    console.log(authorization);\n    return true;\n};\n\n// This function runs after a transaction.\nconst afterTransaction = async (transaction) => {\n    console.log(transaction)\n};\n\n// This function runs after a transaction.\nconst afterDecline = async (transaction) => {\n    console.log(transaction)\n};",
    "centsAmount": "10100",
    "currencyCode": "zar",
    "merchantCode": 7996,
    "merchantName": "USkaka",
    "merchantCity": "Durban",
    "countryCode": "ZA"
}'
```
