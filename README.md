---

## 📱 M-Pesa API Integration Guide

This project integrates **Safaricom M-Pesa** services using the official **Daraja API**, enabling mobile money transactions on your website or application.

---

### 🔗 Useful Links

* 🧰 **Daraja API Portal (Official API Access):**
  [https://developer.safaricom.co.ke](https://developer.safaricom.co.ke)

* 📝 **Register as a Developer with Safaricom:**
  [https://developer.safaricom.co.ke/user/register](https://developer.safaricom.co.ke/user/register)

* 📚 **Official Daraja API Documentation:**
  [https://developer.safaricom.co.ke/daraja/apis/post/transaction-status-query](https://developer.safaricom.co.ke/daraja/apis)

---

## 🔍 Overview of M-Pesa API Services

The Safaricom Daraja API provides multiple transaction types. This project focuses on:

### 1. 📥 Customer to Business (C2B)

Allows customers to **pay your business** using **PayBill** or **Till numbers**.

* ✅ Ideal for collecting payments (e.g. products, services).
* 🔄 Requires you to register confirmation and validation URLs.
* 💬 Receives M-Pesa payment notifications automatically.

#### 🧪 C2B Simulation Tool:

[https://developer.safaricom.co.ke/test\_credentials](https://developer.safaricom.co.ke/test_credentials)

---

### 2. 📤 Business to Customer (B2C)

Allows your business to **send money to customers** directly from your M-Pesa account.

* 🧾 Use cases: salary payments, disbursements, rewards, refunds.
* 🔐 Requires security credentials (initiator name, certificate, encrypted password).

#### 🧾 B2C API Endpoint:

`https://sandbox.safaricom.co.ke/mpesa/b2c/v1/paymentrequest`

---

### 3. 📲 STK Push (Lipa Na M-Pesa Online)

Triggers a prompt on a customer's phone to **enter M-Pesa PIN** and complete payment.

* 🌐 Ideal for e-commerce, subscriptions, apps.
* 🔐 Requires a **shortcode**, **passkey**, and **callback URL**.
* 📞 User receives prompt to authorize payment in real-time.

#### 🧾 STK Push Endpoint:

`https://sandbox.safaricom.co.ke/mpesa/stkpush/v1/processrequest`

---

## 🧪 Using the Sandbox Environment

To test your integration, Safaricom provides a **sandbox** with test credentials.

1. Create an account at:
   [https://developer.safaricom.co.ke/user/register](https://developer.safaricom.co.ke/user/register)

2. Log in and go to **My Apps** → **Create a new App**

   * Enable: `M-Pesa Sandbox`
   * You will get:

     * `Consumer Key`
     * `Consumer Secret`
     * `Shortcode (PayBill or Till)`
     * `Test MSISDN`

---

## 🛠️ Integration Steps

### ✅ Get OAuth Token

Every request to M-Pesa APIs requires an access token.

```http
POST https://sandbox.safaricom.co.ke/oauth/v1/generate?grant_type=client_credentials
Authorization: Basic (base64(consumerKey:consumerSecret))
```

---

### ✅ STK Push Example (JS/Python/Node)

Make sure to pass the correct **passkey**, **timestamp**, and **callback URL**.

```json
{
  "BusinessShortCode": "174379",
  "Password": "<Base64Encoded(ShortCode + PassKey + Timestamp)>",
  "Timestamp": "20250629183515",
  "TransactionType": "CustomerPayBillOnline",
  "Amount": "10",
  "PartyA": "2547xxxxxxxx",
  "PartyB": "174379",
  "PhoneNumber": "2547xxxxxxxx",
  "CallBackURL": "https://yourdomain.com/callback",
  "AccountReference": "Invoice123",
  "TransactionDesc": "Payment for Order"
}
```

---

## 🔐 Register Confirmation & Validation URLs for C2B

Send a POST request to:

```http
POST https://sandbox.safaricom.co.ke/mpesa/c2b/v1/registerurl
```

With this body:

```json
{
  "ShortCode": "600000",
  "ResponseType": "Completed",
  "ConfirmationURL": "https://yourdomain.com/c2b/confirm",
  "ValidationURL": "https://yourdomain.com/c2b/validate"
}
```

---

## 📦 Project Structure (example)

```
mpesa-integration/
├── .env
├── index.js
├── routes/
│   ├── stk.js
│   ├── b2c.js
│   └── c2b.js
├── utils/
│   ├── accessToken.js
│   └── securityCredential.js
└── README.md
```

---

## ✅ Required `.env` Variables

```env
CONSUMER_KEY=your_consumer_key
CONSUMER_SECRET=your_consumer_secret
SHORTCODE=600000
PASSKEY=your_passkey
INITIATOR_NAME=testapi
SECURITY_CREDENTIAL=encrypted_credential
CALLBACK_URL=https://yourdomain.com/callback
```

---

## 🧠 Best Practices

* 🔒 Never expose your consumer secret or security credentials in frontend code.
* 📡 Use HTTPS for all callback URLs.
* 📦 Use official SDKs or handle requests manually with Axios or cURL.
* 🧪 Test thoroughly using sandbox before going live.

---

## 🚀 Go Live Checklist

1. ✅ Apply for production access via Safaricom developer portal.
2. ✅ Replace sandbox URLs with production URLs.
3. ✅ Update credentials with real ShortCode, Initiator, and PassKey.
4. ✅ Ensure your server uses SSL (HTTPS).
5. ✅ Monitor all transactions and callbacks in logs.

---

## 📞 Support

* 📧 [developer@safaricom.co.ke](mailto:developer@safaricom.co.ke)
* 📘 [Safaricom Daraja Docs](https://developer.safaricom.co.ke/daraja/apis)

---

## 🙏 Credits

This project was made possible thanks to the help and mentorship of:

- **[Alvin Kiveu](https://github.com/alvin-kiveu)** – for teaching me how to integrate M-Pesa APIs and explaining Daraja's C2B, B2C, and STK Push processes clearly.

Special thanks to [Alvin Kiveu] for their guidance and support in helping me understand and implement M-Pesa API integration, including C2B, B2C, and STK Push.

Your mentorship made a real difference.
Thank you for your time and support!


Here is the youtube video link: https://youtube.com/playlist?list=PLL9VrPrscsUYv0BGf430fxiHEw5E2gdDV

How to install this projet

1. Clone the project

2. Run npm install

3. Run npm start app.js or nodemon app.js

4. Open your browser and go to http://localhost:3000

5. You can now use the API

How to use the API

1. Go to http://localhost:5000

2. Click on the link you want to use

3. You can now use the API


Support us with the one of following ways

1. Star this project

2. Share this project

3. Follow me on GitHub





