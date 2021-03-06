Creating an Email Campaign
==========================

Creates an email campaign with the specified parameters.

Endpoint
--------

``POST /api/v2/email``

Parameters
----------

.. list-table:: **Required Parameters**
   :header-rows: 1
   :widths: 20 20 40 40

   * - Name
     - Type
     - Description
     - Comments
   * - language
     - string
     - Language of the email campaign
     - Short using 2 letter (ISO-639-1) language codes, e.g. en.
   * - name
     - string
     - Title of the email
     -
   * - fromemail
     - string
     - Email address of the sender
     -
   * - fromname
     - string
     - Name of the sender
     -
   * - subject
     - string
     - Subject of the email
     -
   * - email_category
     - string
     - Category ID that the email is assigned to.
     - Category (see :doc:`email_categories`)
   * - filter
     - int
     - Filter ID for the email
     -
   * - contactlist
     - int
     - Contact list ID for the email
     -
   * - html_source
     - string
     - HTML body of the email
     -
   * - text_source
     - string
     - Text source of the email
     -

.. note::

   Both the *filter* and *contactlist* parameters have to be included, and at least one must always be defined by its
   ID, (i.e. it has to be different from 0 (zero)).

.. list-table:: **Optional Parameters**
   :header-rows: 1
   :widths: 20 20 40 40

   * - Name
     - Type
     - Description
     - Comments
   * - unsubscribe
     - int
     - The email contains an unsubscribe link
     - * 0: false
       * 1: true
   * - browse
     - int
     - The email contain a link to an online version
     - * 0: false
       * 1: true
   * - text_only
     - int
     - The email includes a text only version
     - Can only be used if both an HTML and TEXT source is available
       * 0: false
       * 1: true
   * - cc_list
     - int
     - The contact list ID to include when CCing a copy of the email
     - Only works if the BCC List feature is enabled for the customer.
   * - additional_linktracking_parameters
     - string
     - The additional url parameters that will be added to the url of the tracked links when redirected.
     - Only works if the this feature is enabled for the customer.

Request Example
---------------

.. code-block:: json

   {
     "name": "be_afraid_email",
     "language": "en",
     "subject": "convergence",
     "fromname": "Malekith",
     "fromemail": "malekith@example.com",
     "email_category": "111111111",
     "html_source": "<html>Hello $First Name$...</html>",
     "text_source": "Hello $First Name$...",
     "browse": 0,
     "text_only": 0,
     "unsubscribe": 1,
     "filter": "222222222",
     "contactlist": 0
   }

Result Example
--------------

.. code-block:: json

   {
     "replyCode": 0,
     "replyText": "OK",
     "data":
     {
       "id": 2140
     }
   }

Where:

* *id* is the new email campaign ID

Errors
------

.. list-table:: Possible Error Codes
   :header-rows: 1
   :widths: 20 20 40 40

   * - HTTP Code
     - Reply Code
     - Message
     - Description
   * - 500
     - 1
     - Database connection error
     - An error occurred while saving.
   * - 400
     - 10001
     - Invalid email name
     - The name parameter contains forbidden characters.
   * - 400
     - 10001
     - An email with this name already exists
     - A unique name for the email must be provided.
   * - 400
     - 10001
     - Invalid language
     - For a list of supported languages, see the list of language codes.
   * - 400
     - 10001
     - Invalid value: contactlist
     - The contact list ID must be numeric.
   * - 400
     - 10001
     - Invalid value: filter
     - The filter ID must be numeric.
   * - 400
     - 10001
     - Invalid email address
     - The fromemail must be a valid email address.
   * - 400
     - 10001
     - Invalid value: fromname
     - The fromname parameter contains forbidden characters.
   * - 400
     - 10001
     - Subject must not be empty
     - The subject line must have some content.
   * - 400
     - 10001
     - Invalid value: email_category
     - The email category must be numeric.
   * - 400
     - 10001
     - You must select either a contact list or a filter.
     - A contact list ID or a filter ID must be specified. This error message is returned if either both or none are specified.
   * - 400
     - 10001
     - No content
     - Both the html_source and the text_source are empty.
   * - 403
     - 6031
     - CC feature not enabled
     - If the "BCC List" feature is not enabled, then cc_list cannot be set. Ask for this feature from your Account Manager.
   * - 403
     - 6036
     - Additional tracking parameters are not enabled.
     - If the "Enable additional campaign specific tracking params" feature is not enabled, then
       additional_linktracking_parameters cannot be set. Ask for this feature from your Account Manager.
