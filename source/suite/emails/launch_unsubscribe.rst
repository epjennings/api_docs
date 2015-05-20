Unsubscribing a Contact from an Email Campaign
==============================================

Marks a contact as *unsubscribed* for an email campaign launch so that they will be counted in the campaign statistics. It affects
both the response summary (:doc:`launch_response_summary`) and :doc:`../../suite/exports/export_responses`, and also
enables segmentation based on unsubscription.

It **does not change** the opt-in status of the contact; this must be done separately using an additional API request
(:doc:`../../suite/contacts/contact_update`) if necessary.

.. note:: This endpoint is useful if you:

          * send email campaigns with unsubscribe links to your own website
          * define the user as unsubscribed by updating specific fields in their user profile (e.g. a newsletter flag)
          * generate unsubscribe statistics of specific campaigns (i.e. not from all campaigns)

The unsubscribe link must contain parameters $cid$, $llid$ and $uid$. For the list of possible campaign related
placeholders, see :doc:`../appendices/placeholders`.

Endpoint
--------

``POST /api/v2/email/unsubscribe``

Parameters
----------

.. list-table:: **Required Parameters**
   :header-rows: 1
   :widths: 20 20 40 40

   * - Name
     - Type
     - Description
     - Comments
   * - launch_list_id
     - int
     - ID on the basis of which contacts who clicked on the unsubscribe link can be identified.
       In the case of on event emails, there is no availability limit for the launch_list_id. For batch emails, it lasts for 2 months.
     -
   * - email_id
     - int
     - ID of a specific email
     -
   * - uid
     - string
     - Identifies a contact, a randomly generated string.
     -

*To find these IDs:*
Create a new link which points to the unsubscription page of your website in your campaign. 
You can use $cid$ and $llid$. $cid$ will be replaced with the email_id and $llid$ will be replaced with the
launch_list_id. Please make sure that you track the link in Emarsys suite.
Example: `http://yourwebsite.com/unsubscribe.html?email_id=$cid$&launchlist_id=$llid$`

Request Example
---------------

.. code-block:: json

   {
      "launch_list_id": "111111111",
      "email_id": "222222222"
   }

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
     - 1006
     - Empty parameter(s): [value]
     -
   * - 400
     - 6042
     - No such launch
     -
   * - 400
     - 6025
     - No such campaign
     -
   * - 400
     - 1003
     - Internal error
     - key_id and key_value must uniquely identify a contact to be unsubscribed, otherwise this message is displayed.
