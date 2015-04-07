Updating Email Campaigns
========================

Updates an email campaign with the specified parameters.

Endpoint
--------

``POST /api/v2/email/<email_id>/patch``

Parameters
----------

.. list-table:: **Required Parameters**
   :header-rows: 1
   :widths: 20 20 40 40

   * - Name
     - Type
     - Description
     - Comments
   * - email_id
     - int
     - ID of a specific email
     - Campaign cannot be modified when it has already been launched.

.. list-table:: **Optional Parameters**
   :header-rows: 1
   :widths: 20 20 40 40

   * - Name
     - Type
     - Description
     - Comments
   * - name
     - string
     - Name of the email campaign
     - Empty string is not accepted.
   * - language
     - string
     - Language of the email campaign
     - Has to be expressed using the correct ISO code, e.g. 'en', 'de', etc.
   * - subject
     - string
     - Subject of the email campaign
     - It cannot be empty.
   * - additional_linktracking_parameters
     - string
     - Additional URL parameters that are added to the tracked links URL when redirected.
     - Only works if this feature is enabled for the customer.
   * - text_source
     - string
     - Text source of a custom HTML campaign
     - Only works for custom HTML campaigns.
   * - html_source
     - string
     - Html source of a custom HTML campaign
     - Only works for custom HTML campaigns.

Request Example
---------------

.. code-block:: json

   {
      "emailId": "100018233",
      "name": "asgardian_email",
      "additional_linktracking_parameters": ""
   }

Result Example
--------------

.. code-block:: json

   {
      "replyCode": 0,
      "replyText": "OK",
      "data": {
         "id": "100018233",
         "root_email": "0",
         "language": "en",
         "name": "asgardian_email",
         "created": "2014-12-01 12:46:09",
         "deleted": "",
         "fromemail": "odin@example.com",
         "fromname": "Odin",
         "subject": "Prepare to fight!",
         "email_category": "0",
         "filter": "0",
         "contactlist": "176523015",
         "additional_linktracking_parameters": "",
         "cc_list": 0,
         "html_source": "<html>Hello $First Name$...</html>",
         "text_source": "Hello $First Name$...",
         "unsubscribe": "y",
         "browse": "y",
         "status": "1",
         "api_status": "0",
         "api_error": 0,
         "text_only": "n",
         "source": "userlist"
      }
   }

Where:

* *id* = The internal identifier of the email
* *name* = The name of the email in Suite
* *fromemail* = The sender email address
* *fromname* = The sender name
* *subject* = The email subject line
* *email_category* = The category identifier for this email, for more info see :doc:`../emails/email_categories`.
* *filter* = The filter identifier. Available filters can be retrieved via :doc:`../contacts/segment_list`.
* *contactlist* = The contact list identifier. Contact lists can be retrieved via :doc:`../contacts/contact_list_list`.
* *cc_list* = The ID of the contact list which will receive a copy of the email when sent. Only works if BCC List is enabled.
* *status* = The status of the email, for more info see :doc:`../appendices/email_status`.
* *api_status* = The launch status of the email, for more info see :doc:`../appendices/launch_status`.
* *api_error* = Any specific errors related to the endpoints or methods, for more info see :doc:`../appendices/error_codes`.
* *source* = Where the recipient originated, possible values are: **userlist, profile, api**

Errors
------

.. list-table:: Possible Error Codes
   :header-rows: 1
   :widths: 20 20 40 40

   * - HTTP Code
     - Reply Code
     - Message
     - Description
   * - 400
     - 6004
     - No email ID provided
     -
   * - 400
     - 6023
     - Campaign name already taken
     -
   * - 400
     - 6025
     - No such campaign
     -
   * - 400
     - 6037
     - Campaign is not editable
     - Campaign cannot be modified when it is template-based or it has already been launched.
   * - 400
     - 6038
     - Campaign name is invalid
     - Empty string is not accepted.
   * - 403
     - 6036
     - Additional tracking parameters are not enabled.
     - If the "Enable additional campaign specific tracking params" feature is not enabled, then
       additional_linktracking_parameters cannot be set. Please contact Emarsys support to find out more about this feature.
   * - 400
     - 6039
     - Campaign language is invalid
     - For available languages, see :doc:`../appendices/language_codes`.
   * - 400
     - 6040
     - Campaign subject is invalid
     - Subject of a campaign cannot be empty.
   * - 400
     - 6041
     - Campaign source cannot be changed for template based campaigns
     - Only custom HTML campaigns can have custom text or html source.
