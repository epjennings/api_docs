Unsubscribing a Contact from an Email Campaign
==============================================

Marks a contact as unsubscribed for an email campaign launch so it will be counted in the campaign statistics. It affects
the response summary (:doc:`launch_response_summary`) and :doc:`../../suite/exports/export_responses`, and
makes segmentation based on unsubscribtion possible.

It **does not change** the opt-in status of the contact, this must be done with an additional API request
(:doc:`../../suite/contacts/contact_update`) if necessary.

.. note:: It is useful if you aim at:

          * sending email campaigns with unsubscribe links which target your own website
          * unsubscribing the user by updating specific fields in his user profile (e.g. a newsletter flag)
          * counting the unsubscription for the statistics of the specific campaign, not from all campaigns

In your campaign body, create a new link which points to the unsubscription page of your
website. You can use $cid$, $llid$ and $uid$. $cid$ will be replaced with the email ID, $llid$ with the
launch list ID and $uid$ with the randomly generated contact ID. Example: `http://yourwebsite.com/unsubscribe.html?email_id=$cid$&launchlist_id=$llid$`

For the list of possible campaign related placeholders, see :doc:`../appendices/placeholders`.

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
