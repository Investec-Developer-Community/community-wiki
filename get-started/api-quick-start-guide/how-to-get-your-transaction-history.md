# 🏦 How to get your account, balance, and transaction data

The **Account information API** allows you access to your account and transaction data. It can be used to retrieve things like account details and balances.&#x20;

## **Using Postman**&#x20;

If you’re new to APIs and want to get familiar with using the endpoints, we recommend you create a Postman account (it's free) and use the Postman collections provided to test things out.

{% hint style="info" %}
[**Investec Programmable Banking Postman Collection**](https://www.postman.com/investec-open-api/programmable-banking/overview)

It includes collections for the 🏦 Private Banking, 🧰  Corporate Investment Banking (CIB) and 💳Programmable card APIs.
{% endhint %}

### 1. Get your accounts and account ID with Postman&#x20;

Follow these steps for 🏦 Private Banking and 🧰  CIB, using the appropriate Postman collection and API endpoints as above.&#x20;

1. Ensure  have [authenticated](how-to-authenticate.md) and pasted in your bearer token into the "Variables" tables.
2. Navigate to the **Accounts** folder and the **GET Accounts** **query**
3. Hit **Send** to make a call to the account information API endpoint (no additional parameters need to be set).&#x20;

```
🏦 https://openapi.investec.com/za/pb/v1/accounts
🧰 https://openapi.investec.com/za/bb/v1/accounts
```

{% hint style="info" %}
The Accounts query will returns **accountID** as well as **account balance** for 🧰  CIB.
{% endhint %}

The JSON response will include all of your accounts and each account has a unique ID (**accountID**) that you will use when transacting against it.&#x20;

<details>

<summary>Example response for 🏦 Private Banking</summary>

<pre class="language-json"><code class="lang-json"><strong>{
</strong>  "data": {
    "accounts": [
      {
        <a data-footnote-ref href="#user-content-fn-1">"accountId": "1234567890",</a>
        "accountNumber": "11223344556677",
        "accountName": "Jane Smith",
        "referenceName": "Jane Smith",
        "productName": "Private Bank Account",
        "kycCompliant": true,
        "profileId": "9876543210"
      },
    ]
  },
  "links": {
    "self": "https://openapi.investec.com/za/pb/v1/accounts"
  },
  "meta": {
    "totalPages": 1
  }
}
</code></pre>

</details>

<details>

<summary>Example response for 🧰  CIB</summary>

```json
{
    "data": {
        "accounts": [
            {
                "AccountHolderAddress": {
                    "AddressLine1": "",
                    "AddressLine2": "",
                    "City": "",
                    "Country": "",
                    "CountryCode": ""
                },
                "RoutingBIC": "",
                "BankAccountProductType": "",
                "CreditLastCycleToNextBusinessDate": "0001-01-01T00:00:00",
                "CustomerAccountType": "",
                "DebitLastCycleToNextBusinessDate": "0001-01-01T00:00:00",
                "DueDateOfPayment": "2023-05-14T22:00:01Z",
                "MinimumAmountLimit": 0,
                "NumberOfCardHolders": 0,
                "CreditLimit": 1,
                "DebitAccountBankName": "",
                "PendingTransactions": 0,
                "Banks": {
                    "Name": "Investec South Africa",
                    "ChipsUID": "",
                    "Branch": [
                        {
                            "Number": ""
                        }
                    ],
                    "PostalAddress": {
                        "AddressLine1": "",
                        "AddressLine2": "",
                        "City": "",
                        "Country": null
                    }
                },
                "Currencies": {
                    "CurrencyCode": "ZAR"
                },
                "InterestDistribution": "",
                "NoticesBalance": 0,
                "AccountOpenDate": "2021-07-01T22:00:01Z",
                "CumulativeNoticesAmount": 0,
                "InstantAvailableNoticeBalance": 0,
                "MinimimAmountLimit": 0,
                "loggedOnUser": {
                    "UserFirstName": "John",
                    "UserLastName": "Doe",
                    "UserCompany": "John Doe (Pty) Ltd"
                },
                "NoticeInterestNominated": 0,
                "NoticeInterestBank": "",
                "noticeInterestAccountName": "",
                "NoticeInterestAccount": "",
                "PreviousStatementPeriod": "2023-01-01T22:00:01Z",
                "DebitAccountNumber": "",
                "DealReference": "",
                "AutomaticPaymentOrder": "0",
                "BackOfficeCustomerCode": "JDCARD",
                "AccountId": "10111",
                "AccountName": "10011111111 Credit Card",
                "AccountFullName": "",
                "AccountType": "Credit Card",
                "AccountTypeId": "1",
                "AccountNumber": "10011111111",
                "AlternativeAccNo": "",
                "ElectronicAccountNumber": "",
                "Balances": {
                    "CapitalBalance": 100,
                    "AvailableBalance": 100,
                    "PrincipalAmount": 0,
                    "ValueDate": "2023-01-01T22:00:01Z",
                    "ClosingBalance": 200,
                    "PendingCardBalance": 0
                },
                "BackOfficeType": "",
                "Products": {
                    "StartDate": "0001-01-01T00:00:00",
                    "EndDate": "0001-01-01T00:00:00",
                    "OverdraftLimit": 0,
                    "MaxTransferLimit": 0
                },
                "Description": "Credit Card",
                "OwnerType": "1",
                "Interests": {
                    "Amount": 0,
                    "Rate": 0,
                    "RateMaturity": 0,
                    "RateCredit": 0,
                    "RateDebit": 10,
                    "AccruedCreditInterest": 0,
                    "AccruedDebitInterest": 0
                },
                "ActiveFlag": "Y",
                "NickName": "Credit Card",
                "CreatedDate": "2021-07-01T22:00:01Z",
                "ModifiedDate": "0001-01-01T00:00:00",
                "MaturityAmount": 0,
                "StatementFrequency": "",
                "StatementNumber": "",
                "StatementDay": "0",
                "StatementMonth": "",
                "EmailAddress": "",
                "Category": "Borrow",
                "LinkedAccount": "",
                "AccountFormat": "4"
            }
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

### 2. Get your account balance with Postman

Follow these steps for 🏦 Private Banking using the appropriate Postman collection and API endpoints as above. **The account balance for 🧰 CIB is included in the Get Accounts request.**

1. Retrieve the accountID from your previous call to get accounts.
2. Head over to the "Variables" table to insert your accountID. You can also set it under the Params tab on the query page.&#x20;
3. Navigate to the **Accounts** folder and the **GET Account Balance query** .
4. Hit **Send** to make a call to the API endpoint.

```
🏦  https://openapi.investec.com/za/pb/v1/accounts/:accountId/balance
```

<details>

<summary>Example response for 🏦 Private Banking</summary>

```json
{
    "data": {
        "accountId": "3353431574710163189587446",
        "currentBalance": 33607.16,
        "availableBalance": 33607.16,
        "currency": "ZAR"
    },
    "links": {
        "self": "https://openapisandbox.investec.com/za/pb/v1/accounts/3353431574710163189587446/balance"
    },
    "meta": {
        "totalPages": 1
    }
}
```

</details>

### 3. Get your transaction data with Postman&#x20;

Follow these steps for 🏦 Private Banking and 🧰 CIB, using the appropriate Postman collection and API endpoints as above.&#x20;

1. Ensure you have added your accountID to the "Variables" table&#x20;
2. Navigate to the **GET Account transactions** query and set the dates for which you would like to view the transactions by selecting **fromDate** and **toDate** in the **Query params table** and adding the dates.&#x20;
3. fromDate and toDate can be any  formatted [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date \[Example of formatted date: 1999-09-09]].
4. Hit **Send** to make a call to the API endpoint.

<pre><code><strong>🏦  https://openapi.investec.com/za/pb/v1/accounts/:accountId/transactions?fromDate=2023-03-10&#x26;toDate=2023-03-10
</strong>🧰  https://openapi.investec.com/za/bb/v1/accounts/:accountId/transactions?fromDate=2023-01-01&#x26;toDate=2023-01-31
</code></pre>

<details>

<summary>Example response for 🏦 Private Bank</summary>

```json
{
    "data": {
        "transactions": [
            {
                "accountId": "3353431574710163189587446",
                "type": "DEBIT",
                "transactionType": "CardPurchases",
                "status": "POSTED",
                "description": "KURUMAN FRESH PRODUCE H KURUMAN ZA",
                "cardNumber": "402261xxxxxx0011",
                "postedOrder": 11049,
                "postingDate": "2023-04-13",
                "valueDate": "2023-04-30",
                "actionDate": "2023-04-12",
                "transactionDate": "2023-04-11",
                "amount": 53.6,
                "runningBalance": 34679.66
            },
            {
                "accountId": "3353431574710163189587446",
                "type": "DEBIT",
                "transactionType": "CardPurchases",
                "status": "POSTED",
                "description": "YOCO   *ARUKAH HEALTH KURUMAN ZA",
                "cardNumber": "402261xxxxxx0018",
                "postedOrder": 11050,
                "postingDate": "2023-04-13",
                "valueDate": "2023-04-30",
                "actionDate": "2023-04-12",
                "transactionDate": "2023-04-12",
                "amount": 374,
                "runningBalance": 34305.66
            },
           
        ]
    },
    "links": {
        "self": "https://openapisandbox.investec.com/za/pb/v1/accounts/3353431574710163189587446/transactions"
    },
    "meta": {
        "totalPages": 1
    }
}
```

</details>

<details>

<summary>Example response for 🧰  CIB</summary>

<pre class="language-json"><code class="lang-json"><strong>{
</strong>    "data": {
        "transactions": [
            {
                "AccountName": "ZAR 1900539687921 SmartRate Plus Notice 32",
                "TransactionCode": "9",
                "TransactionStatus": "approved",
                "InvestmentDate": "0001-01-01T00:00:00",
                "InvestmentDateUtc": "0001-01-01T00:00:00",
                "InvestmentDateSa": "0001-01-01T01:52:00+01:52",
                "InvestmentName": null,
                "InvestmentStatus": null,
                "RemainingTerm": null,
                "InvestmentAmount": null,
                "StatementId": "52292",
                "InstantAccessBalance": null,
                "BranchCode": null,
                "AccountNumber": null,
                "DistributionAccount": null,
                "AccountType": null,
                "PostDate": "0001-01-01T00:00:00",
                "PostDateUtc": "0001-01-01T00:00:00",
                "PostDateSa": "0001-01-01T01:52:00+01:52",
                "Interest": null,
                "AccruedInterest": null,
                "MaturityDate": "0001-01-01T00:00:00",
                "MaturityDateUtc": "0001-01-01T00:00:00",
                "MaturityDateSa": "0001-01-01T01:52:00+01:52",
                "BankName": null,
                "CustomerReferenceId": "",
                "BackOfficeReferenceId": "",
                "CardNumber": "92974054603",
                "TransactionId": "202304110000000000009",
                "Reference": "DVfZ WT tmKkeb",
                "Beneficiaries": {
                    "LinkList": null,
                    "Entities": {
                        "EntityName": "aQaZUGJXQuCqxwJX JoYk ftvSWKWybWXPS OZVmxIq"
                    }
                },
                "Description": "X bssSCS",
                "Accounts": {
                    "AccountId": 91974,
                    "AccountNumber": "1900539687921"
                },
                "Currencies": {
                    "CurrencyCode": "ZAR"
                },
                "CaptureDate": "2023-07-19T18:25:33.83Z",
                "CaptureDateUtc": "2023-07-19T18:25:33.83Z",
                "CaptureDateSa": "2023-07-19T20:25:33.83+02:00",
                "ValueDate": "2023-07-19T18:25:33.83Z",
                "ValueDateUtc": "2023-07-19T18:25:33.83Z",
                "ValueDateSa": "2023-07-19T20:25:33.83+02:00",
                "CardHolderName": "mj TgW VOGbTQo",
                "AutoForwardProcessingDate": false,
                "Amount": -130000000,
                "Reference_1": "99162191",
                "Reference_2": "",
                "Reference_3": "MAECrNWJfonnjpifiJDlhUBtixrq kMHnf",
                "Reference_4": null,
                "Reference_5": null,
                "Reference_8": "665",
                "Reference_9": "gUDASgs t pwqHBeowNZBJwJkEGIMdEErHJXocDrXTfbeIRRjF srDkOAdOxUvfWnsCFhSZLKkxJ TyMlYXsoCDyP USlHaNRRMwItGdxJrP",
                "Reference_10": "",
                "RunningBalance": 19290794.77
            },
            {
                "AccountName": "ZAR 1900539687921 SmartRate Plus Notice 32",
                "TransactionCode": "10",
                "TransactionStatus": "approved",
                "InvestmentDate": "0001-01-01T00:00:00",
                "InvestmentDateUtc": "0001-01-01T00:00:00",
                "InvestmentDateSa": "0001-01-01T01:52:00+01:52",
                "InvestmentName": null,
                "InvestmentStatus": null,
                "RemainingTerm": null,
                "InvestmentAmount": null,
                "StatementId": "52311",
                "InstantAccessBalance": null,
                "BranchCode": null,
                "AccountNumber": null,
                "DistributionAccount": null,
                "AccountType": null,
                "PostDate": "0001-01-01T00:00:00",
                "PostDateUtc": "0001-01-01T00:00:00",
                "PostDateSa": "0001-01-01T01:52:00+01:52",
                "Interest": null,
                "AccruedInterest": null,
                "MaturityDate": "0001-01-01T00:00:00",
                "MaturityDateUtc": "0001-01-01T00:00:00",
                "MaturityDateSa": "0001-01-01T01:52:00+01:52",
                "BankName": null,
                "CustomerReferenceId": "",
                "BackOfficeReferenceId": "",
                "CardNumber": "",
                "TransactionId": "202304300000000000010",
                "Reference": "",
                "Beneficiaries": {
                    "LinkList": null,
                    "Entities": {
                        "EntityName": "hdPZPMq "
                    }
                },
                "Description": "VpXcXPsq",
                "Accounts": {
                    "AccountId": 91974,
                    "AccountNumber": "1900539687921"
                },
                "Currencies": {
                    "CurrencyCode": "ZAR"
                },
                "CaptureDate": "2023-08-07T18:25:33.83Z",
                "CaptureDateUtc": "2023-08-07T18:25:33.83Z",
                "CaptureDateSa": "2023-08-07T20:25:33.83+02:00",
                "ValueDate": "2023-08-07T18:25:33.83Z",
                "ValueDateUtc": "2023-08-07T18:25:33.83Z",
                "ValueDateSa": "2023-08-07T20:25:33.83+02:00",
                "CardHolderName": "",
                "AutoForwardProcessingDate": false,
                "Amount": 1313801.71,
                "Reference_1": "",
                "Reference_2": "",
                "Reference_3": "",
                "Reference_4": null,
                "Reference_5": null,
                "Reference_8": "797",
                "Reference_9": "vPqivetP",
                "Reference_10": "",
                "RunningBalance": 20604596.48
            },
            {
                "AccountName": "ZAR 1900539687921 SmartRate Plus Notice 32",
                "TransactionCode": "11",
                "TransactionStatus": "approved",
                "InvestmentDate": "0001-01-01T00:00:00",
                "InvestmentDateUtc": "0001-01-01T00:00:00",
                "InvestmentDateSa": "0001-01-01T01:52:00+01:52",
                "InvestmentName": null,
                "InvestmentStatus": null,
                "RemainingTerm": null,
                "InvestmentAmount": null,
                "StatementId": "52342",
                "InstantAccessBalance": null,
                "BranchCode": null,
                "AccountNumber": null,
                "DistributionAccount": null,
                "AccountType": null,
                "PostDate": "0001-01-01T00:00:00",
                "PostDateUtc": "0001-01-01T00:00:00",
                "PostDateSa": "0001-01-01T01:52:00+01:52",
                "Interest": null,
                "AccruedInterest": null,
                "MaturityDate": "0001-01-01T00:00:00",
                "MaturityDateUtc": "0001-01-01T00:00:00",
                "MaturityDateSa": "0001-01-01T01:52:00+01:52",
                "BankName": null,
                "CustomerReferenceId": "",
                "BackOfficeReferenceId": "",
                "CardNumber": "",
                "TransactionId": "202305310000000000011",
                "Reference": "",
                "Beneficiaries": {
                    "LinkList": null,
                    "Entities": {
                        "EntityName": "pZwWKoPA"
                    }
                },
                "Description": " tqwoyld",
                "Accounts": {
                    "AccountId": 91974,
                    "AccountNumber": "1900539687921"
                },
                "Currencies": {
                    "CurrencyCode": "ZAR"
                },
                "CaptureDate": "2023-09-07T18:25:33.83Z",
                "CaptureDateUtc": "2023-09-07T18:25:33.83Z",
                "CaptureDateSa": "2023-09-07T20:25:33.83+02:00",
                "ValueDate": "2023-09-08T18:25:33.83Z",
                "ValueDateUtc": "2023-09-08T18:25:33.83Z",
                "ValueDateSa": "2023-09-08T20:25:33.83+02:00",
                "CardHolderName": "",
                "AutoForwardProcessingDate": false,
                "Amount": 1076307.1,
                "Reference_1": "",
                "Reference_2": "",
                "Reference_3": "",
                "Reference_4": null,
                "Reference_5": null,
                "Reference_8": "",
                "Reference_9": " HT icGG",
                "Reference_10": "",
                "RunningBalance": 21680903.58
            },
            {
                "AccountName": "ZAR 1900539687921 SmartRate Plus Notice 32",
                "TransactionCode": "12",
                "TransactionStatus": "approved",
                "InvestmentDate": "0001-01-01T00:00:00",
                "InvestmentDateUtc": "0001-01-01T00:00:00",
                "InvestmentDateSa": "0001-01-01T01:52:00+01:52",
                "InvestmentName": null,
                "InvestmentStatus": null,
                "RemainingTerm": null,
                "InvestmentAmount": null,
                "StatementId": "52372",
                "InstantAccessBalance": null,
                "BranchCode": null,
                "AccountNumber": null,
                "DistributionAccount": null,
                "AccountType": null,
                "PostDate": "0001-01-01T00:00:00",
                "PostDateUtc": "0001-01-01T00:00:00",
                "PostDateSa": "0001-01-01T01:52:00+01:52",
                "Interest": null,
                "AccruedInterest": null,
                "MaturityDate": "0001-01-01T00:00:00",
                "MaturityDateUtc": "0001-01-01T00:00:00",
                "MaturityDateSa": "0001-01-01T01:52:00+01:52",
                "BankName": null,
                "CustomerReferenceId": "",
                "BackOfficeReferenceId": "",
                "CardNumber": "",
                "TransactionId": "202306300000000000012",
                "Reference": "",
                "Beneficiaries": {
                    "LinkList": null,
                    "Entities": {
                        "EntityName": "lAxjcVbg"
                    }
                },
                "Description": "gLeRJPbl",
                "Accounts": {
                    "AccountId": 91974,
                    "AccountNumber": "1900539687921"
                },
                "Currencies": {
                    "CurrencyCode": "ZAR"
                },
                "CaptureDate": "2023-10-07T18:25:33.83Z",
                "CaptureDateUtc": "2023-10-07T18:25:33.83Z",
                "CaptureDateSa": "2023-10-07T20:25:33.83+02:00",
                "ValueDate": "2023-10-08T18:25:33.83Z",
                "ValueDateUtc": "2023-10-08T18:25:33.83Z",
                "ValueDateSa": "2023-10-08T20:25:33.83+02:00",
                "CardHolderName": "",
                "AutoForwardProcessingDate": false,
                "Amount": 1103322.74,
                "Reference_1": "",
                "Reference_2": "",
                "Reference_3": "",
                "Reference_4": null,
                "Reference_5": null,
                "Reference_8": "",
                "Reference_9": "rIYXgXSU",
                "Reference_10": "",
                "RunningBalance": 22784226.32
            }
        ]
    },
    "links": {
        "self": "https://openapisandbox.investec.com/za/bb/v1/accounts/91974/transactions"
    },
    "meta": {
        "TotalCount": 4,
        "TotalPages": 1,
        "CurrentPage": 1,
        "CurrentPageSize": 100,
        "ResultCount": 4
    }
}
</code></pre>

</details>

{% hint style="info" %}
**Pro Tips:**

* You may have noticed, the endpoint accepts a pagination parameter for when you need to iterate through a longer transaction history.
* Filtering can be done using the **postingdate**
  * **postingdate** is the date at which the transaction affects your balance
  * **transactiondate** is the date on which the transaction took place (day the card was physically swiped)
{% endhint %}

## **cuRL code snippets**

### 🏦 **Private Banking**

#### Get accounts and accountID&#x20;

```
curl --location 'https://openapi.investec.com/za/pb/v1/accounts' \
--header 'Accept: application/json'
```

#### Get account balance

```
curl --location 'https://openapi.investec.com/za/pb/v1/accounts//balance' \
--header 'Accept: application/json'
```

#### Get transaction data

```
curl --location 'https://openapi.investec.com/za/pb/v1/accounts//transactions' \
--header 'Accept: application/json'
```

### 🧰 **CIB**&#x20;

#### Get accounts,  accountID and account balance&#x20;

```
curl --location 'https://openapi.investec.com/za/bb/v1/accounts' \
--header 'Accept: application/json' \
--header 'Authorization: [[Authorization-masked-secret]]'
```

#### Get transaction data

```
curl --location 'https://openapi.investec.com/za/bb/v1/accounts/<<account id>>/transactions?fromDate=2023-01-01&toDate=2023-01-31' \
--header 'Accept: application/json' \
--header 'Authorization: [[Authorization-masked-secret]]'
```

[^1]: 
