Unsubscribing a Contact from an Email Campaign
==============================================

Flags a contact as unsubscribed for an email campaign launch so they will included in the campaign statistics. It affects
the response summary (:doc:`launch_response_summary`) and :doc:`../../suite/exports/export_responses`, as well as making
segmentation based on unsubscription possible.

Unsubscribing the contact from an email campaign **does not change** the opt-in status of the contact. Opt-in changes must be performed using an additional API request
(:doc:`../../suite/contacts/contact_update`) if necessary.

.. note:: This endpoint is useful if you intend to:

          * send email campaigns with unsubscribe links which target your own website
          * unsubscribe a contact by updating specific fields in their user profile (e.g. a newsletter flag)
          * count the unsubscription statistics of a specific campaign (not from all campaigns)

In your campaign body, create a new link which points to the unsubscription page of your
website. You can include any of the following additional placeholders: $cid$, $llid$ and $uid$. 

$cid$ will be replaced with the email ID, $llid$ with the launch list ID and $uid$ with the randomly generated contact ID. Example: `http://yourwebsite.com/unsubscribe.html?email_id=$cid$&launchlist_id=$llid$`

For a complete list of campaign related placeholders, see :doc:`../appendices/placeholders`.

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
     - ID used to identify which contacts clicked the unsubscribe link.
       When using batch emails, the data is available for 2 months only. In the case of on-event emails there is no limit for the launch_list_id data availability.
     -
   * - email_id
     - int
     - ID of a specific email
     -
   * - uid
     - string
     - Identifies a contact; is displayed as a randomly generated string.
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
