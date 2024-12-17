# 👤 How to authenticate against the Investec API

{% embed url="https://www.loom.com/share/4c0281f1621a4fbb8886547bb38aa4ee" %}

### **Authentication**&#x20;

Before you go ahead and query the Investec banking API for things like account and transaction data, you will first need to authenticate.&#x20;

* The APIs use a modified version of the OAuth 2.0 standard and requires an **api key** as a header in the auth request, in addition to your client ID and client secret.
* In response to the auth request you will receive a secure access token, called a **bearer token**, which needs to be used in all your API calls.&#x20;
* **Bearer tokens are valid for 30 minutes and therefore need to be refreshed**.&#x20;

### cURL Code Snippet

```
curl --location 'https://openapi.investec.com/identity/v2/oauth2/token' \
--header 'x-api-key: <<your api_key>>' \
--header 'Accept: application/json' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Authorization: [[Authorization-masked-secret]]' \
--data-urlencode 'grant_type=client_credentials'
```

### **Using Postman**&#x20;

If you’re new to APIs and want to get familiar with using the endpoints, we recommend you create a Postman account (it's free) and use the Postman collections provided to test things out.

{% hint style="info" %}
[**Investec Programmable Banking Postman Collection**](https://www.postman.com/investec-open-api/programmable-banking/overview)

It includes collections for the 🏦 Private Banking, 🧰  Corporate Investment Banking and 💳Programmable card APIs.
{% endhint %}

* Once you’ve signed up for an account, head over to these collections and make sure you **fork the collection that is relevant to you.**

### 1. Authentication using Postman

Follow the same steps for  🏦 Private Banking, 🧰  CIB.&#x20;

**Endpoint:**

```
https://openapi.investec.com/identity/v2/oauth2/token
```

1. Head over to the "Variables" tab to set your environment variables for ease of use.
2. Insert your **client ID**, **client secret** and **api key.**
3. Navigate to the Auth folder, and the **POST Authentication query**.
4. The Auth type is set to **Basic Auth** (using basic authentication headers)
5. Your headers include the **x-api-key header** which uses your api key&#x20;
6. In the request body,  the **grant-type** field has the value **client\_credentials**

We expect that in response to your client id, secret and key, the endpoint will respond with a secure token, called a **bearer token.**&#x20;

7. Hit **Send** on your request&#x20;

If your keys are valid, the response will contain the token and an expiration when you send the request.

**Example response**

```json
{
  "access token": "qwertyuiop123456789",
  "token_type": "Bearer",
  "expires_in": "1799",
  "scope": "accounts",
 }
```

### 2. Making API calls following authentication

* Copy the bearer token and paste it into your environment variables  table so that you can use it in all your requests going forward.&#x20;
* It needs to be given the designation bearer in requests&#x20;
* Remember the bearer token is valid for 30 minutes, at which point you will need to request a new one by calling the same endpoint again.&#x20;
