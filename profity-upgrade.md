# Upgrading from Profity to Sovendus Voucher Network

This guide details the steps required to upgrade your integration from Profity to Sovendus. Follow these instructions to replace your current Profity scripts on both the Order Success/Thank You page and the landing page with the new Sovendus integration. Detailed testing instructions using our browser plugin are also provided.

---

## 1. Previous Integration Setup

Before upgrading, your current Profity integration looks like this:

### Order Success/Thank You Page

```html
<script async src="https://domain/clients/conversion.js?s=PROFITY_ID&ordervalue=%orderValue%&ordernumber=%orderNumber%&vouchercode=%voucherCode%"></script>
```

### Landing Page

```html
<script async src="https://domain/clients/main.js"></script>
```

---

## 2. New Sovendus Integration

Replace the above Profity scripts with the following Sovendus code.

### A. Order Success/Thank You Page

#### 1. Add the Container Markup

Place the following `<div>` in your Order Success/Thank You page where you want the Sovendus content to load. (Note that the placement of this container does not affect the positioning of the Sovendus sticky banner or overlay.)

```html
<div id="sovendus-container-1">
  <!-- Sovendus integration loads content into this div -->
</div>
```

#### 2. Insert the Integration Script

Add the following script at the end of your `<body>` section. Make sure to replace the placeholder values with your actual data:

- **YOUR_TRAFFIC_SOURCE_NUMBER**: Your Sovendus traffic source number.
- **YOUR_TRAFFIC_MEDIUM_NUMBER**: Your Sovendus traffic medium number.
- **Session-ID**, **Timestamp**, **Order-ID**, **Order value**, **Order currency**, **Used coupon code**: Replace these with dynamic values from your system.
- **Customer data placeholders**: Replace with the appropriate customer information.

```html
<!--sovendus code begin -->
<script type="text/javascript">
  window.sovIframes = window.sovIframes || [];
  window.sovIframes.push({
    trafficSourceNumber: YOUR_TRAFFIC_SOURCE_NUMBER,  // Replace with your Sovendus traffic source number
    trafficMediumNumber: YOUR_TRAFFIC_MEDIUM_NUMBER,  // Replace with your Sovendus traffic medium number
    sessionId: "Session-ID",                          // Replace with your session identifier
    timestamp: "Timestamp",                           // Replace with the current timestamp
    orderId: "Order-ID",                              // Replace with your dynamic order ID
    orderValue: "Order value",                        // Replace with your dynamic order value
    orderCurrency: "Order currency",                  // Replace with the currency code (e.g., "USD")
    usedCouponCode: "Used coupon code",               // Replace with the coupon code if applicable
    iframeContainerId: "sovendus-container-1",
    integrationType: "genericScript-1.3.4"
  });
  window.sovConsumer = {
    consumerSalutation: "Salutation ('Mr.' or 'Mrs.')", // Replace with customer salutation
    consumerFirstName: "First name",                     // Replace with customer first name
    consumerLastName: "Last Name",                       // Replace with customer last name
    consumerEmail: "client address (e-mail address)",    // Replace with customer email address
    consumerStreet: "client address (street)",           // Replace with street name
    consumerStreetNumber: "client address (house number)", // Replace with house number
    consumerZipcode: "client address (zip code)",        // Replace with postal code
    consumerCity: "client address (city)",               // Replace with city name
    consumerCountry: "client address (Country)",         // Replace with country name
    consumerPhone: "client phone number",                // Replace with customer phone number
    consumerYearOfBirth: "client year of birth",         // Replace with customer's birth year
    consumerDateOfBirth: "client date of birth"          // Replace with customer's full date of birth
  };
  // Append Sovendus script to the head
  var script = document.createElement("script");
  script.type = "text/javascript";
  script.async = true;
  script.src = "https://api.sovendus.com/sovabo/common/js/flexibleIframe.js";
  document.head.appendChild(script);
</script>
<!--sovendus code end -->
```

---

### B. Landing Page

Replace the old Profity landing page script with the following Sovendus landing page script:

```html
<script async="true" src="https://api.sovendus.com/js/landing.js"></script>
```

---

## 3. Testing Your Integration

After updating your integration:

- **Install the Browser Plugin:** Use the Sovendus browser plugin to simulate the Sovendus environment on your pages. This tool helps you preview the integration and troubleshoot any issues.
  
- **Review the Testing Documentation:** For detailed instructions on how to test and validate your integration, please refer to the [Sovendus Testing Docs](https://api.sovendus.com/docs/testing).

---

## 4. Platform-Specific Plugins and Components

For an even easier integration experience, we recommend checking out our range of plugins and components that are designed specifically for your platform. These solutions streamline the setup process by reducing manual configuration.  
Find the right plugin or component for your platform here: [Sovendus Plugins & Components](https://api.sovendus.com/plugins).

---

By following these steps, you will successfully upgrade your integration from Profity to Sovendus Voucher Network. Make sure to replace all placeholder values with your dynamic data to ensure proper functionality. Happy integrating!
