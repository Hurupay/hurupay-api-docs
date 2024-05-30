Webhooks
========

.. _webhooks:
Webhooks Overview
^^^^^^^^^^^^^^^^
Webhooks enable you to create a notification system to receive updates on specific requests made to the Collection and Payout API services.

When the status of your API calls changes, the Hurupay resource server sends updates to your server via webhooks. This status change is referred to as an event, which you usually listen for on a POST endpoint.

A webhook URL is essentially a POST endpoint where a resource server sends updates. This URL must parse a JSON request and respond with a status OK.

To receive webhooks on your server, you must update your webhook settings for the specific environments (e.g., `sandbox and production`) in the `dashboard <https://dashboard.hurupay.com/>`_ under settings, depending on which environment you are using.

.. code-block:: javascript
    :caption: Express.js Example of a webhook endpoint to handle collection updates

    router.post("/collection/webhook/url", function(req, res) {
    // Retrieve the request's body
    const event = req.body;
    console.log(event)
    res.send(200);
    });

Collections Webhooks
--------------------

Failed collection webhook
~~~~~~~~~~~~~~~~~~~~~
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

Successfull collection webhook
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
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

Payouts Webhooks
--------------------

Failed payout webhook
~~~~~~~~~~~~~~~~~~~~~

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


Successfull payout webhook
~~~~~~~~~~~~~~~~~~~~~~~~~

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
                "FiatAmount": "10"
                }
            }
        }
    }