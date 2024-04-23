# Sovendus generic documentation for Voucher Network and Checkout Benefits

## Introduction Voucher Network

This documentation is intended to help you successfully integrate Sovendus Voucher Network and/or Checkout Benefits into your shop.

The implementation is done via JavaScript on the shop’s order success page. An iFrame is used to connect to the Sovendus servers to retrieve the individual reward banner and embed it on the page. At the same time, the successful voucher redemption is transmitted to Sovendus.

Your personal banner and/or list with special offers will be created by Sovendus and made available on our servers.

If you have any questions or encounter any issues during the process, please do not hesitate to reach out to us for assistance.

## Integrating Sovendus on Your Order Success/Thank You Page

### 1. Place the HTML Markup

Copy the HTML markup provided into the appropriate location in your order success/thank you page's HTML code. This code creates a container where the Sovendus content will be loaded. The position of this container doesn't affect the placement of the Sovendus sticky banner and overlay if you're using one.

```html
<div id="sovendus-container-1">
  <!-- the integration loads the content into this div element -->
</div>
```

### 2. Replace Placeholder Variables

Replace the placeholder variables ({$TRAFFIC_SOURCE_NUMBER} and {$TRAFFIC_MEDIUM_NUMBER}) with the actual traffic source number and traffic medium number you have received from Sovendus.

### 3. Insert JavaScript Code

Copy the HTML code below and paste it into the end of the <body> section of your order success/thank you page. This code initializes the Sovendus integration and provides necessary data about the order and the consumer.

```html
<!--sovendus code begin -->
<script type="text/javascript">
  window.sovIframes = window.sovIframes || [];
  window.sovIframes.push({
    trafficSourceNumber: "{$TRAFFIC_SOURCE_NUMBER}",
    trafficMediumNumber: "{$TRAFFIC_MEDIUM_NUMBER}",
    sessionId: "Session-ID",
    timestamp: "Timestamp",
    orderId: "Order-ID",
    orderValue: "Order value",
    orderCurrency: "Order currency",
    usedCouponCode: "Used coupon code",
    iframeContainerId: "sovendus-container-1",
    integrationType: "genericScript-1.3.0",
  });
  window.sovConsumer = {
    consumerSalutation: "Salutation ('Mr.' or 'Mrs.')",
    consumerFirstName: "First name",
    consumerLastName: "Last Name",
    consumerEmail: "client address (e-mail address)",
    consumerStreet: "client address (street)",
    consumerStreetNumber: "client address (house number)",
    consumerCountry: "client address (Country)",
    consumerZipcode: "client address (zip code)",
    consumerPhone: "client phone number",
    consumerYearOfBirth: "client year of birth",
  };
  // Append Sovendus script to the body
  var script = document.createElement("script");
  script.type = "text/javascript";
  script.async = true;
  script.src =
    window.location.protocol +
    "//api.sovendus.com/sovabo/common/js/flexibleIframe.js";
  document.body.appendChild(script);
</script>
<!--sovendus code end -->
```

### 4. Customize Consumer Data

Ensure that the sovConsumer and sovIframes objects contains actual data about the consumer / order. Replace the placeholder values ("Salutation", "First name", etc.) with the corresponding data retrieved from your order form or user database. You can find [more information about the parameters here](https://github.com/Sovendus-GmbH/Sovendus-Voucher-Network-and-Checkout-Benefits-Parameter)

### 5: Test the Integration

After implementing the code, test your order success/thank you page to ensure that the Sovendus integration works as expected and that the content is loaded.

## Additional steps for Switzerland

For Switzerland it is also required to add the following script to your home page / the page where users coming from Sovendus will land on:

### Variant 1 - add the script via JavaScript

To add the script via JavaScript just add the following script to the home / landing page:

```javascript
var script = document.createElement("script");
script.type = "text/javascript";
script.async = true;
script.src = "https://api.sovendus.com/js/landing.js";
document.head.appendChild(script);
```

### Variant 2 - add the script into HTML

Just add the following to the HTML of the home / landing page:

```html
<script async="true" src="https://api.sovendus.com/js/landing.js"></script>
```
