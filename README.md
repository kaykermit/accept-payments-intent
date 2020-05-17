# Accepting a card payment

This is a Stripe integration of Payment Intents - One-time Payments.
It includes `using-webhooks` integration, which enables accepting cards issued in regions outside of U.S. and Canada, where you will need to handle requests from banks to authenticate a purchase (commonly known as 3DS or OTP).



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

This code includes a Node implementation of Accept Payment Intents [using-webhooks](/using-webhooks) integration.

Follow these proposed steps below to run locally.

**1. Clone or download the project**

To get the Stripe API Keys, crate and log in to your Stripe account in order to run this project.
Once you log in to your account, go to the Stripe [developer dashboard](https://stripe.com/docs/development#api-keys) to find your API keys.
```
STRIPE_PUBLISHABLE_KEY=<replace-with-your-publishable-key>
STRIPE_SECRET_KEY=<replace-with-your-secret-key>
```

**2. Follow the server instructions on how to run:**

Run the Node server in `accept-payments-intent`:

```
cd accept-payments-intent/server
npm install
npm start
```

**3. Run a webhook locally:**

If you want to test the integration with a local webhook on your machine, you can use the Stripe CLI to easily spin one up.

First [install the CLI](https://stripe.com/docs/stripe-cli) and [link your Stripe account](https://stripe.com/docs/stripe-cli#link-account).

```
stripe listen --forward-to localhost:4242/webhook
```

The CLI will print a webhook secret key to the console. Set `STRIPE_WEBHOOK_SECRET` to this value in your .env file.

You should see events logged in the console where the CLI is running.

When you are ready to create a live webhook endpoint, follow our guide in the docs on [configuring a webhook endpoint in the dashboard](https://stripe.com/docs/webhooks/setup#configure-webhook-settings).

**4. Set up the web client app:**

Launch the web client implementation by typing in the local host web address in a browser to run.

When the app is running, use `4242424242424242` as a test card number with any CVC code + a future expiration date.

Use the `4000000000003220` test card number to trigger a 3D Secure challenge flow. You should see all tests listed here pass
t https://stripe.com/docs/testing.


## Author

kaykermit
