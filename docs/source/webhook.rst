Webhooks
========

Webhooks: Real-time Transaction Updates
---------------------------------------

Webhooks Overview
^^^^^^^^^^^^^^^^^
**Imagine** knowing the status of your transactions the moment they happen—no refreshing, no waiting. With **Hurupay's Webhooks**, you can create a dynamic notification system that keeps you in the loop on all your **Collection** and **Payout API** activities.

When the status of your API calls changes, Hurupay’s resource server **immediately** notifies your server via webhooks. This status change, known as an event, triggers a notification that you can handle through a POST endpoint.

A webhook URL is essentially a **POST endpoint** that your server listens to for updates. It must be able to parse a JSON request and respond with a status OK to acknowledge receipt. 

For both **On Ramp** and **Off Ramp** transactions, it’s essential to have webhooks set up to capture the final status—whether success or failure. **And here’s the best part:** you can configure more than one webhook URL, tailoring the experience to your needs.

.. code-block:: javascript
    :caption: Express.js Example of a Webhook Endpoint to Handle Collection Updates

    router.post("/collection/webhook/url", function(req, res) {
        // Retrieve the request's body
        const event = req.body;
        console.log(event)
        res.status(200).send('OK');
    });

Partner Webhooks
----------------

Ready to set up your webhooks? Let’s dive in:

Request Headers
~~~~~~~~~~~~~~~
Your webhook interactions require the following headers:

.. code-block:: javascript

    headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${your-api-key}`
    }

Create Webhook
~~~~~~~~~~~~~~
Start by creating a new webhook:

.. code-block:: console

    POST https://sandbox.hurupay.com/v1/webhook

**Request Body**

Here’s how your request body should look:

.. code-block:: javascript

    {
        "url":"https://webhook.site/3c7493b3-f8a3-4fae-834e-00611345d056"
    }

**Request Response**

Upon a successful creation, you’ll receive the following response:

.. code-block:: javascript
    
    {
        "success": true,
        "message": "Webhook created successfully",
        "data": {
            "partnerId": "66bc4d75d8deec854010a9a9",
            "url": "https://webhook.site/3c7493b3-f8a3-4fae-834e-00611345d050",
            "status": "active",
            "_id": "66bd5387bd8c03f82ad87dcf"
        }
    }

List All Webhooks
~~~~~~~~~~~~~~~~~
Curious to see all your webhooks? Use this command:

.. code-block:: console

    GET https://sandbox.hurupay.com/v1/webhook

**Request Response**

Here’s the response showing your existing webhooks:

.. code-block:: javascript

    {
        "success": true,
        "message": "Webhooks fetched successfully",
        "data": [
            {
                "_id": "66bc52460d68a57141ef2aa5",
                "partnerId": "66bc4d75d8deec854010a9a9",
                "url": "https://webhook.site/3c7493b3-f8a3-4fae-834e-00611345d056",
                "status": "disabled"
            },
            {
                "_id": "66bc52a54885955790f70c8c",
                "partnerId": "66bc4d75d8deec854010a9a9",
                "url": "https://webhook.site/3c7493b3-f8a3-4fae-834e-00611345d056",
                "status": "active"
            },
            {
                "_id": "66bd5387bd8c03f82ad87dcf",
                "partnerId": "66bc4d75d8deec854010a9a9",
                "url": "https://webhook.site/3c7493b3-f8a3-4fae-834e-00611345d050",
                "status": "active"
            }
        ]
    }

Find Webhook by ID
~~~~~~~~~~~~~~~~~~
Looking for a specific webhook? Here's how:

.. code-block:: console

    GET https://sandbox.hurupay.com/v1/webhook/{webhookId}

**Request Response**

Retrieve details about the specified webhook:

.. code-block:: javascript

        {
            "success": true,
            "message": "Webhook fetched successfully",
            "data": {
                "_id": "66bc52460d68a57141ef2aa5",
                "partnerId": "66bc4d75d8deec854010a9a9",
                "url": "https://webhook.site/3c7493b3-f8a3-4fae-834e-00611345d056",
                "status": "disabled"
            }
        }

Enable or Disable Webhook
~~~~~~~~~~~~~~~~~~~~~~~~~
Need to toggle a webhook’s status? Here’s how:

.. code-block:: console

    PUT https://sandbox.hurupay.com/v1/webhook/{webhookId}

**Request Body**

Set the status to "active" or "disabled":

.. code-block:: javascript

    {
        "status":"active"
    }

**Request Response**

Confirmation of the status change:

.. code-block:: javascript
    
        {
            "success": true,
            "message": "Webhook status updated successfully",
            "data": {
                "_id": "66bc52460d68a57141ef2aa5",
                "partnerId": "66bc4d75d8deec854010a9a9",
                "url": "https://webhook.site/3c7493b3-f8a3-4fae-834e-00611345d056",
                "status": "active"
            }
        }

Delete Webhook
~~~~~~~~~~~~~~
Ready to clean up? Deleting a webhook is simple:

.. code-block:: console

    DELETE https://sandbox.hurupay.com/v1/webhook/{webhookId}

**Request Response**

You’ll receive a confirmation like this:

.. code-block:: javascript

        {
            "success": true,
            "message": "Webhook deleted successfully",
            "data": {}
        }

On & Off Ramp Webhook Responses
-------------------------------

Failed Onramp/Collection Webhook
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Here’s what a failed collection webhook response looks like:

.. code-block:: javascript

    {
    "Body": {
        "collectionCallback": {
        "PartnerRequestID": "66386452d8d95fb8b8870859",
        "CollectionRequestID": "73436b14-b6f5-4e9e-bb4f-aaf605294467",
        "ResultCode": 0,
        "ResultDesc": "Transaction process was cancelled!"
        }
    }
    }

Successful Onramp/Collection Webhook
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
And here’s a successful collection response:

.. code-block:: javascript

        {
        "Body": {
            "collectionCallback": {
            "PartnerRequestID": "66386452d8d95fb8b8870859",
            "CollectionRequestID": "e3e73daf-e257-4f90-9077-291471ec6157",
            "ResultCode": 1,
            "ResultDescription": "The service request is processed successfully.",
            "PaymentData": {
                "PhoneNumber": "254704407239",
                "FiatCurrency": "KES",
                "FiatAmount": 10,
                "CryptoSymbol": "cUSD",
                "CryptoDeposited": 0.0727,
                "WalletAddressDeposited": "0x67279306F1e188FD6bEE167203E1bE49661755Bf",
                "TransactionReceipt": "https://explorer.celo.org/alfajores/tx/0x9cd65d15d7a621544dd36b587a45f4492ee282d1a8810ca8aaf347bbdc505395"
                }
              }
            }
        }

Failed Payout Webhook
~~~~~~~~~~~~~~~~~~~~~
Example of a failed payout webhook:

.. code-block:: javascript

    {
        "Body": {
            "payoutCallback": {
            "PartnerRequestID": "66386452d8d95fb8b8870859",
            "PayoutRequestRequestID": "1f886740-b902-414f-adc2-1d7eb7fa5465",
            "ResultCode": 0,
            "ResultDesc": "Invalid transaction submitted for processing"
            }
        }
    }

Successful Payout Webhook
~~~~~~~~~~~~~~~~~~~~~~~~~
Example of a successful payout webhook:

.. code-block:: javascript

    {
        "Body": {
            "payoutCallback": {
            "PartnerRequestID": "66386452d8d95fb8b8870859",
            "PayoutRequestRequestID": "d193e73b-0f1a-4228-8f70-cbd799738b87",
            "ResultCode": 1,
            "ResultDescription": "The service request is processed successfully.",
            "PaymentData": {
                "PhoneNumber": "254704407239",
                "FiatCurrency": "KES",
                "FiatAmount": 10,
                "CryptoSymbol": "cUSD",
                "CryptoDeducted": 0.0727,
                "WalletAddressDeducted": "0x67279306F1e188FD6bEE167203E1bE49661755Bf",
                "TransactionReceipt": "https://explorer.celo.org/alfajores/tx/0x9cd65d15d7a621544dd36b587a45f4492ee282d1a8810ca8aaf347bbdc505395"
                }
              }
            }
        }
    }
