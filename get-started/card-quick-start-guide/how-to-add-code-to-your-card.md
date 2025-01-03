# 🖥️ How to add code to your card and run a simulation using the online IDE

## The Investec Online IDE

The **Investec Online IDE (integrated development environment)** enables Investec Private Banking clients to execute custom functionality on your programmable card.&#x20;

1. Navigate to the Investec Developer homepage by clicking on **“Manage”**, followed by **“Investec Developer”**.&#x20;
2. Click on **“manage code”** on the Programmable Card IDE tile.&#x20;
3. You will be presented with a list of your cards. Ensure it is enabled by toggling the card on.&#x20;
4. Click on the card to which you would like to add your code.&#x20;
5. The IDE or code editor for your card will open up, ready for you to start adding your code.

{% hint style="info" %}
**Pro-Tip:** The IDE can be slow to load and you might need to refresh the page.
{% endhint %}

## Adding code to your card via the IDE and running a simulation

There are three main functions that can be used to execute custom functionality on your card:

* **`beforeTransaction`**&#x20;
  * Every time you initiate a transaction from your Investec card, the **beforeTransaction** method intercepts the authorisation before it is approved by Investec.&#x20;
  * This gives you the ability to apply logic to **either decline or approve the transaction based on data from the card authorization** itself.&#x20;
  * This function needs to **return a true or false value** in order for it to work.&#x20;
  * Time is limited for this function so use minimal code.
* **`afterTransaction`**&#x20;
  * This function will execute after every transaction that has been processed by the card.&#x20;
* **`afterDecline`**&#x20;
  * This function will execute if a transaction has been declined on the card.

1. Navigate to the **main.js file** and paste in the code snippet below to test.&#x20;
   1. The code snippet declines card purchases that are made in bakeries (using a specified merchant code) and that are over R50 (or 5000 cents).
2. Click **"Save changes".** By doing so it won't have an effect on your card until you click "deploy code to card"

````javascript
// ```javascript
const beforeTransaction = async (authorization) => {
  if (authorization.merchant.category.key === 'bakeries') {
    return authorization.centsAmount < 5000
  }
  return true
}
```
````

{% hint style="info" %}
**Pro-Tip:** When referring to amounts in the code it is the **cent value** of the transaction. R55 equals 5500 cents.
{% endhint %}

3. Navigate to the right-hand side of the code editor to the simulator. The simulator allows you to simulate transactions to test out the code on your card before you deploy it.&#x20;
4. Type in a value of 5100 cents (R51.00), which is above the R50 limit we have set with the code.&#x20;
5. Click "**Simulate card transaction".**&#x20;
6. A **simulation.json** file will be created, showing that the transaction failed (**authorizationApproved** will be false) because the amount is over the limit specified.&#x20;
7. Once you have tested the code and would like to deploy the code to the card click "**Deploy code to card**".&#x20;

{% hint style="info" %}
**Pro-Tip:** The **log.json**  file shows all the logs from the code. You can also log certain outcomes using the **console.log** function.
{% endhint %}
