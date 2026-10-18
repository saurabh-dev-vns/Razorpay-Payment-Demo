# Razorpay Payment Demo

A small payment demo built with Node.js, Express, and Razorpay Checkout. The page lets a user enter an amount and contact details, creates an order on the server, and verifies the payment signature on the server.

## Requirements

- Node.js and npm
- A Razorpay account with API keys (use Test Mode while developing)

## Setup

1. Install the dependencies:

   ```bash
   npm install
   ```

2. Create a local `.env` file from the example:

   **Windows PowerShell**

   ```powershell
   Copy-Item .env.example .env
   ```

   **macOS/Linux**

   ```bash
   cp .env.example .env
   ```

3. Open `.env` and replace the placeholders with your Razorpay **Test Mode** Key ID and Key Secret:

   ```env
   RAZORPAY_KEY_ID=rzp_test_your_key_id
   RAZORPAY_KEY_SECRET=your_key_secret
   PORT=3000
   ```

   Get API keys from the Razorpay Dashboard under **Account & Settings → API Keys**. Keep `.env` private; it is excluded from Git. Only the example file with placeholders should be committed.

4. Start the server:

   ```bash
   npm start
   ```

   For automatic restarts during development, run `npm run dev`.

5. Visit [http://localhost:3000](http://localhost:3000).

## Try a test payment

Enter an amount and optionally provide name, email, and phone. Choose a test payment method in Razorpay Checkout and use the current test instructions for that method from [Razorpay's documentation](https://razorpay.com/docs/payments/payments/test-card-details/).

## Payment flow

1. The browser sends the amount to `POST /api/create-order`.
2. The server creates a Razorpay order and returns the order details and public Key ID.
3. Razorpay Checkout collects the payment details.
4. The browser sends the Checkout response to `POST /api/verify-payment`.
5. The server checks the payment signature using the Key Secret.

## API routes

| Method | Route | Purpose |
| --- | --- | --- |
| `GET` | `/` | Serves the payment page |
| `POST` | `/api/create-order` | Creates a Razorpay order |
| `POST` | `/api/verify-payment` | Verifies the payment signature |
| `GET` | `/api/payment/:paymentId` | Fetches payment details from Razorpay |

## Security note

This project is a learning/demo integration, not a complete production payment system. Never expose the Key Secret in frontend code or commit real credentials. Before using payments in production, add appropriate input validation, error handling, HTTPS, and server-side order/payment state management.
