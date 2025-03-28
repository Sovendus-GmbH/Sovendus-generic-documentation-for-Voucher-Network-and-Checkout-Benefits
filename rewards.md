# Sovendus generic documentation for Rewards

## Introduction Rewards

This documentation is intended to help you successfully integrate Sovendus Rewards into your shop.

The implementation is done via JavaScript on the shop’s order success page. An iFrame is used to connect to the Sovendus servers to retrieve the individual reward banner and embed it on the page.

Your personal banner and/or list with special offers will be created by Sovendus and made available on our servers.

If you have any questions or encounter any issues during the process, please do not hesitate to reach out to us for assistance.

## Integrating Sovendus on your user profile page

### 1. Place the HTML Markup

Copy the HTML markup provided into the appropriate location in your user profile page's HTML code. This code creates a container where the Sovendus content will be loaded. The position of this container doesn't affect the placement of the Sovendus sticky banner and overlay if you're using one.

```html
<div id="sovendus-container-1">
  <!-- the integration loads the content into this div element -->
</div>
```

### 2. Replace Placeholder Variables

Replace the placeholder variables TRAFFIC_SOURCE_NUMBER and TRAFFIC_MEDIUM_NUMBER with the actual traffic source number and traffic medium number you have received from Sovendus.

### 3. Insert JavaScript Code

Copy the HTML code below and paste it into the end of the <body> section of your user profile page. This code initializes the Sovendus integration and provides necessary data about the consumer.

```html
<!--sovendus code begin -->
<script type="text/javascript">
  window.sovIframes = window.sovIframes || [];
  window.sovIframes.push({
    trafficSourceNumber: YOUR_TRAFFIC_SOURCE_NUMBER,
    trafficMediumNumber: YOUR_TRAFFIC_MEDIUM_NUMBER,
    iframeContainerId: "sovendus-container-1",
    integrationType: "genericScript-1.3.4",
  });
  window.sovConsumer = {
    consumerSalutation: "Salutation ('Mr.' or 'Mrs.')",
    consumerFirstName: "First name",
    consumerLastName: "Last Name",
    consumerEmail: "client address (e-mail address)",
    consumerStreet: "client address (street)",
    consumerStreetNumber: "client address (house number)",
    consumerZipcode: "client address (zip code)",
    consumerCity: "client address (zip code)",
    consumerCountry: "client address (Country)",
    consumerPhone: "client phone number",
    consumerYearOfBirth: "client year of birth",
    consumerDateOfBirth: "client date of birth",
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

### 4. Customize Consumer Data

Ensure that the sovConsumer objects contains actual data about the consumer. Replace the placeholder values ("Salutation", "First name", etc.) with the corresponding data retrieved from your user profile or user database.

### 5: Test the Integration

After implementing the code, test your user profile page to ensure that the Sovendus integration works as expected and that the content is loaded.