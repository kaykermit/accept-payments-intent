# Accepting a card payment

This is a Stripe integration of Payment Intents - One-time Payments.
It uses a webhooks integration to enable accepting cards (issued in regions outside of U.S. and Canada) that may require extra authentication (commonly known as 3DS or OTP). Cards issued in U.S. and Canada do not usually need this extra authentication.



|     | Using webhooks 
:--- | :---
**Recommended for** | Businesses with a global customer base who want to add other payment methods  
**Bank authentication requests** | Automatically handles, no need for extra code  
**Payment flow** | Server -> Client 
**Webhooks for post-payment fulfillment** | Recommended (scales better to future payment method) 



**Test**

Use the below test card numbers with any CVC code + a future expiration date to test for certain behavior.

| Test card number     | Using webhooks
:--- | :---
**4242424242424242** | Succeeds 
**4000000000003220** | Displays a pop-up modal to authenticate 


## How to run locally

This project is a Node implementation of Accept Payment Intents integration.

Follow these proposed steps below to run locally.

**1. Clone or download the project**

Clone or download the project. Open the project folder. You need to rename a file called envfile in the server folder to **.env** and add the Stripe API keys and Webhook Secret to this .env file before you run the project.

To get the required Stripe API Keys, create and log in to your Stripe account. 

Go to the Stripe [developer dashboard](https://stripe.com/docs/development#api-keys) to find your API keys.

```
STRIPE_PUBLISHABLE_KEY=<replace-with-your-publishable-key>
STRIPE_SECRET_KEY=<replace-with-your-secret-key>
```

**2. Run a webhook locally:**

To get the required Webhook Secret that will enable you to test the Stripe integration on your machine, you need to use Stripe CLI. 

Follow [steps 1 and 2 on this link](https://stripe.com/docs/stripe-cli) to install Stripe CLI and link your Stripe account

```
stripe login
```

Then get the webhook secret key by running this command.

```
stripe listen --forward-to localhost:4242/webhook
```

The CLI will print a webhook secret key to the console. Go back to your .env file, and set `STRIPE_WEBHOOK_SECRET` to this value in the .env file.

You should see events logged in the console where the CLI is running.


**3. Follow these server instructions on how to run:**

Run the Node server in `accept-payments-intent`:

```
cd accept-payments-intent/server
npm install
npm start
```


**4. Set up the web client app:**

Launch the web client implementation by typing in the local host web address in a browser to run.

When the app is running, run the tests stated earlier:

Use `4242424242424242` as a test card number with any CVC code + a future expiration date.

Use the `4000000000003220` test card number to trigger a 3D Secure challenge flow. 

You should see all tests listed here pass.


## Author

kaykermit
