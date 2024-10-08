# 💸 How to make a payment

{% embed url="https://www.loom.com/share/733e3023bc8844e186e1752134570527" %}

In addition to retrieving historical data from your account, the Investec 🏦 Private Banking API allows you to programmatically make payments to beneficiaries on your account. This functionality is not yet available on the 🧰 CIB API.

Let’s explore how to make a payment to an existing beneficiary on your account using the community-contributed [**Postman Collection**](https://god.gw.postman.com/run-collection/26868804-00260d55-0009-42ee-b148-d439992e64ff?action=collection%2Ffork\&collection-url=entityId%3D26868804-00260d55-0009-42ee-b148-d439992e64ff%26entityType%3Dcollection%26workspaceId%3D905c2bab-81a1-4297-8b70-2456c776a7a0).

{% hint style="info" %}
**Pro-Tip:** You can only make programmatic payments to beneficiaries that have been paid at least once before with regular online banking from your account.
{% endhint %}

As with accounts, every beneficiary on your banking profile also has a unique ID. You can retrieve the list of beneficiaries from the following endpoint: https://openapi.investec.com/za/pb/v1/accounts/beneficiaries. Again, you use a bearer token for authentication as with all API requests to the Investec API, and a typical response has the following structure:

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

The [Postman Collection](https://god.gw.postman.com/run-collection/26868804-00260d55-0009-42ee-b148-d439992e64ff?action=collection%2Ffork\&collection-url=entityId%3D26868804-00260d55-0009-42ee-b148-d439992e64ff%26entityType%3Dcollection%26workspaceId%3D905c2bab-81a1-4297-8b70-2456c776a7a0) has a request for this named Beneficiaries (in the Beneficiaries folder)

Now that you have a beneficiary ID, let’s make a small payment to them. For that, we’ll be using https://openapi.investec.com/za/pb/v1/accounts/{accountId}/paymultiple.

The endpoint receives an array list of payments, as it’s able to process multiple payments at one point. Payments are easily defined and have four key fields:

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

The [Postman collection](https://god.gw.postman.com/run-collection/26868804-00260d55-0009-42ee-b148-d439992e64ff?action=collection%2Ffork\&collection-url=entityId%3D26868804-00260d55-0009-42ee-b148-d439992e64ff%26entityType%3Dcollection%26workspaceId%3D905c2bab-81a1-4297-8b70-2456c776a7a0) has a Beneficiary Payment request you can use to try this out for yourself.

As you will see, you have full programmatic control of the process and it does not require additional manual verification.
