---
title: How Beveel Works?
permalink: docs/how_beveel_works.html
toplevel: Overview
---

Overview of Recommendations Renderization
-----------------------------------------

The rendering of recommendations on a page works in the following way:

* Customer inserts beveel.js in the web page, configuring the javascript snippet like shown under the configuration 'Code Snippet' section
* When a user visits a page where beveel.js is present a request is sent to Beveel with the current page URL as one of the parameters
* Beveel then searches for any pageConfigurations that match their 'Page URL Pattern' with the current page URL parameter received
* Then we look for any active experiments for each one of the pageConfigurations found
* Beveel responds this first request with the list of pageConfigurations and experiments
* beveel.js checks each experiment and randomly assigns the user to a particular audience based on the 'Total Traffic', ' Original Traffic' and 'Variant Traffic' values
* Once we know which version should be rendered, a new request is made to Beveel with the pageConfiguration or variant id to be queried along with any evaluated 'dynamic' parameters required by the underlying template
* Beveel checks its cache to see if the particular recommendation was already returned previously and if not, queries the DB for the product ids to be returned, retrieves each product from the catalog, retrieves the pre compiled HTML template and applies the list of products to the template, returning the HTML snippet to be inserted in the page. The cache is updated in this case
* beveel.js receives the HTML snippet to be inserted for each matching pageConfiguration or variant and inserts them on the page according the configured 'Location'. At this point each product URL received is modified to include Beveel's specific attributes so we can track effectiveness of recommendations
