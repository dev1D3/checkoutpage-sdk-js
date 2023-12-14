# 1D3 Javascript package

### What is it?

It is package that will help you with generating payment URL according to 
[1D3 documentation](https://docs.1d3.com/en/en_PP_Integration.html).

### How to use?

#### Get checkout page URL

1. Install the package (with your package manager):
```shell
npm install 1d3-sdk
yarn add 1d3-sdk
```

2. Require somewhere in your code, set parameters and get the URL:
```javascript
const { Payment } = require('1d3-sdk');

// create Payment object with your account ID and secret salt
const e = new Payment('112', 'my_secret');

// set payment details 
e.paymentAmount = 1000;
e.paymentId = 'FFCD12-30';
e.paymentCurrency = 'USD';

// set another parameters, like success or fail callback URL, customer details, etc.

// get payment URL
const url = e.getUrl();
```

Now your can render payment `url` somewhere on your checkout page.

#### Receive callback from 1D3

Example with [Express](http://expressjs.com):
```javascript
const { Callback } = require('1d3-sdk');

app.post('/payment/callback', function(req, res) {
  const callback = new Callback('secret', req.body);
  if (callback.isPaymentSuccess()) {
    const paymentId = callback.getPaymentId();
    // here is your code for success payment
  }
});
```
Note that `Callback` constructor throws Error if signature isn't valid.
