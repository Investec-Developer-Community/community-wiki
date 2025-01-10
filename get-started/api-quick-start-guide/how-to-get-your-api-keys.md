# 🔑 How to create your API keys

{% embed url="https://www.loom.com/share/28eda68190434b8fb96285f530777987" %}

{% hint style="info" %}
Before you begin, ensure you are enrolled for Investec Developer on your Private Banking or CIB account (see [Investec Developer self enrollment guide](https://investec.gitbook.io/programmable-banking-community-wiki/get-started/self-enrollment-guide)).&#x20;
{% endhint %}

## Client ID, client secret and API keys

* To start using the Investec API, you must first get your credentials - your client ID and secret.&#x20;
* In addition, you'll need to create an api key.
* API keys specify the bank account you want to access via the API as well as which permissions or functionality you want to access (ie. I want to be able to access my transaction data, but don't want to be able to make payments).
* We use a combination of your client ID, client secret and api key to authenticate your requests so that you can transact securely against your Investec account.&#x20;

## Access your client ID, client secret and create new API keys

### 🏦 **Private Banking accounts**

1. Login to Investec Online and click on “Manage”, followed by Investec Developer.&#x20;
2. Select “Individual Connections”. You will be able to view your credentials (client ID and secret) and any API keys you have created for your account here.&#x20;
3. Click on “Create new API key”.
4. Name your API key by entering a name under “Alias”&#x20;
5. Select the account(s) for which you would like to grant the API keys to access to.&#x20;
6. Select the permissions for which you would like the API keys to have access to.&#x20;
   1. Your account name and number
   2. Your account balance
   3. Your transactions
   4. Your inter account transfers
   5. Allow beneficiary payments
   6. View statements
   7. View tax certificates
   8. View and update card code&#x20;
7. Select continue to create your API key. The new API key will now be available on the Individual Connections page.&#x20;

**Only the main account holder will have access to credentials and have the ability to create new API keys.**&#x20;

### 🧰 CIB accounts

1. Login to Investec Online and click on “Investec Developer”.
2. Select “Business Connections”.  You will be able to view your credentials (client ID and secret) and any API keys you have created for the app that you have connected. You can toggle between connected apps.&#x20;
3. Click on “Create new API key”.
4. Name your API key by entering a name under “Alias”.
5. Select the companies that the key will have access to&#x20;
6. Select the permissions for which you would like the API keys to have access to.
   1. Your account name and number
   2. Your transactions
   3. View and update card code
7. Select continue to create your API key. The new API key will now be available on the Business Connections page.

