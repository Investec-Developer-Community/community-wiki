# 💸 How to make transfers and payments

{% embed url="https://www.loom.com/share/733e3023bc8844e186e1752134570527" %}

The **Account information API** also allows Investec clients to perform actions against their account programmatically (not just read-only). This includes transferring money between your accounts and paying money to beneficiaries. &#x20;

{% hint style="info" %}
Transfers and payments are currently only available for 🏦 Private Banking account holders.&#x20;
{% endhint %}

## **Using Postman**&#x20;

If you’re new to APIs and want to get familiar with using the endpoints, we recommend you create a Postman account (it's free) and use the Postman collections provided to test things out.

{% hint style="info" %}
[**Investec Programmable Banking Postman Collection**](https://www.postman.com/investec-open-api/programmable-banking/overview)
{% endhint %}

### 1. Make a transfer

1. [Retrieve a list of your accounts and their accountIDs](how-to-get-your-transaction-history.md#id-1.-get-your-accounts-and-account-id-with-postman)
2. &#x20;Take note of the **accountID** that you would like to make the transfer to.
3. Navigate to the **Accounts folder** and **POST transfer multiple query.**
4. Head over to the "Variables" table to insert your **accountID - this is the account from which you would like to make the transfer.** You can also set it under the Params tab on the query page.
5. Navigate to the **Body** tab and enter a value into each field. Here you will see that each transfer is defined by four key fields
   1. **beneficiaryAccountID -** this is the account where the funds will transfer to
   2. **amount** - the amount to pay in ZAR
   3. **myReference** - reference displayed on your transaction description
   4. **theirReference** - reference displayed on the recipients statement

```json
{
    "transferList": [
        {
            "beneficiaryAccountId": "3353431574710166878182963",
            "amount": "10", 
            "myReference": "API transfer",
            "theirReference": "API transfer"
        }
    ] 
}
```

6. Hit **Send** to make a call to the API endpoint.

<pre><code><strong>https://openapi.investec.com//za/pb/v1/accounts/:accountId/transfermultiple
</strong></code></pre>

### 2. Make a payment

{% hint style="info" %}
**You can only make programmatic payments to beneficiaries that have been created and paid at least once before from your account with regular online banking. Beneficiary payments are limited to R20 000.00.**
{% endhint %}

1. Retrieve your list of beneficiaries by navigating to the **Beneficiaries** folder and the **GET Beneficiaries query**.&#x20;
2. Ensure you have [authenticated](how-to-authenticate.md) and pasted in your bearer token into the "Variables" tables.
3. Hit **Send** to make a call to the API endpoint (no additional parameters need to be set).&#x20;

```
https://openapi.investec.com/za/pb/v1/accounts/beneficiaries
```

4. Take note of the **beneficiaryID** of the beneficiary that you would like to make the payment to.&#x20;

<details>

<summary>Example response for 🏦 Private Banking</summary>

```json
{
  "data": [
    {
      "beneficiaryId": "LOREMIPSUMDOLOR=",
      "accountNumber": "1234567890",
      "code": "123456",
      "bank": "ACME CORP",
      "beneficiaryName": "Jane Smith",
      "lastPaymentAmount": "1.00",
      "lastPaymentDate": "10/01/2023",
      "cellNo": null,
      "emailAddress": null,
      "name": "Jane Smith",
      "referenceAccountNumber": "LOREM IPSUM DOLOR",
      "referenceName": "LOREM IPSUM",
      "categoryId": "112233445566",
      "profileId": "77889900"
    },
  ],
  "links": {
    "self": "https://openapi.investec.com/za/pb/v1/accounts/beneficiaries"
  },
  "meta": {
    "totalPages": 1
  }
}
```

</details>

{% hint style="info" %}
Payment notifications will go out to the listed "cellNo" and "emailaddress" of the beneficiary. If these are null, then no notification will be sent.
{% endhint %}

5. Navigate to **Beneficiaries** folder and the **POST Beneficiary payment query.** The endpoint can receive an array list of payment and is therefore able to process multiple payments at one point.&#x20;
6. Head over to the "Variables" table to insert your **accountID - this is the account from which you would like to make the payment.** You can also set it under the Params tab on the query page.
7. Navigate to the **Body** tab and enter a value into each field. Here you will see that each payment is defined by four key fields
   1. **beneficiaryID -** this is the account to which you want to make the payment
   2. **amount** - the amount to pay in ZAR
   3. **myReference** - reference displayed on your transaction description
   4. **theirReference** - reference displayed on the recipients statement

```json
{
  "paymentsList": [
    {
      "beneficiaryId": "01234567890",
      "amount": "10",
      "myReference": "API transfer",
      "theirReference": "API transfer"
    }
  ]
}
```

5. Hit **Send** to make a call to the API endpoint.&#x20;

```
https://openapi.investec.com/za/pb/v1/accounts/{accountId}/paymultiple
```

## cURL code snippets

#### Get beneficiaries

```
curl --location 'https://openapi.investec.com/za/pb/v1/accounts/beneficiaries' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json'
```

#### Get beneficiary categories

```
curl --location 'https://openapi.investec.com/za/pb/v1/accounts/beneficiarycategories' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json'
```

#### **Make a transfer**&#x20;

```
curl --location 'https://openapi.investec.com/za/pb/v1/accounts//transfermultiple' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data '{
    "transferList": [
        {
            "beneficiaryAccountId": "3353431574710166878182963", 
            "amount": "10", 
            "myReference": "API transfer", 
            "theirReference": "API transfer" 
        }
    ] 
}'
```

#### Make a payment

```
curl --location 'https://openapi.investec.com/za/pb/v1/accounts//paymultiple' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data '{
    "paymentList": [
        {
            "beneficiaryId": "{{beneficiaryId}}", 
            "amount": "10", 
            "myReference": "API demo", 
            "theirReference": "API demo2" 
        }
    ]
}'
```

