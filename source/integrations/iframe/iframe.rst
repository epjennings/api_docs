Single Sign-on
==============

We provide an integration point where your service can be integrated with Suite as a page.
This involves adding a new menu entry and loading your page content within an iframe. The design of your page
should ideally match the Suite design, so it will look like it is part of the Suite.

Some browsers like Safari and Internet Explorer blocks setting cookies in "third-party" iframes. In our case,
it would make cookie based session handling impossible, and session handling generally hard. The solution is
that on loading the integration's Suite page, Suite will redirect the browser to the integration's login URL,
allowing it to create the session cookie. It will send customer information, and a redirect URL, where the
integration have to redirect back the browser. On that page we are going to load the iframe of the integration,
and display it to the customer.

Checklist
---------

We have created a checklist regarding the required information to enable the Single Sign-On for your convenience.
Please send the following information to your contact person:

* The name of your service
* The login URL - it have to create a session, and redirect the customer back to Suite to the provided URL
* The iframe URL - it will be loaded into the iframe

Login Parameters
----------------

As a first step, we redirect the browser to the login URL, and providing the following query parameters (the request
will be also presigned with Escher):

.. list-table:: **Parameters**
   :header-rows: 1
   :widths: 30 20 40

   * - Parameter Name
     - Type
     - Description
   * - environment
     - string
     - Host name of the customer’s Suite environment (e.g. login.emarsys.net)
   * - customer_id
     - int
     - ID of the customer in the Suite database
   * - admin_id
     - int
     - ID of the admin
   * - redirect_to
     - string
     - URL where the integration have to redirect the customer to

Useful Resources
----------------

We recommend checking out the following resources. Querying the timezone (for displaying time information
in the customer's timezone) or the name of a customer might be useful for a service.

* :doc:`../../suite/customers/customer_settings`
