Collections (On Ramp)
====================

.. _mobile_money:

On Ramp Mobile Money
-------------------

Overview
^^^^^^^^
The API service facilitates seamless integration of various mobile money wallets and mobile services across listed countries. It supports notable providers such as Safaricom, Airtel,MTN, TIGO enabling clients to streamline the process of converting local currencies into equivalent stablecoin dollars. This service is designed to assist with on-ramping, ensuring a smooth transition into the digital currency ecosystem.

.. note::
   The mobile money service is currently available in:

   * `Kenya (MPESA)`,
   * `Ghana (MTN,VODAFONE,TIGO,AIRTEL)`,
   * `Tanzania (MTN, VODACOM, TIGO, AIRTEL)`, 

Base URL

The BASE URL is https://sandbox.hurupay.com/v1

Authentication
^^^^^^^^^^^^^^
The collection API uses partner's apikey **(sandbox key or production key)**. Include your `partner api key` in each request headers to the API.

Endpoints
^^^^^^^^^

1. POST /collections/mobile/initialize_transaction
~~~~~~~~~

Overview
~~~~~~~
This endpoint is used to facilitate the deposit of digital assets or tokens to a user's wallet address. The phone number provided in the request body will receive a request-to-pay prompt. If the user successfully completes the request, Hurupay will credit the user's wallet address with the respective amount of digital assets, both provided in the request body. The token amount is determined according to Hurupay's :doc:`exchange_rates` API Service.

POST Request URL 
~~~~~~~~~
.. raw:: html

      <p style="color: red;">https://sandbox.hurupay.com/v1/collections/mobile/initialize_transaction</p>

Request Headers
~~~~~~~~~

.. code-block:: javascript

    headers: {
        "Content-Type": "application/json"
        Authorization: `Bearer ${Api-Key}`,
    }

Request Body
~~~~~~~~~

.. code-block:: javascript

   {
        "collection": {
            "customerName": "John Doe",
            "customerEmail": "johndoe@gmail.com",
            "phoneNumber": "+2547XXXXXX",
            "countryCode": "KE",
            "network": "MPESA",
            "amount":1000
        },
        "transfer":{
            "digitalNetwork":"CELO",
            "digitalAsset":"cUSD",
            "walletAddress":"0xD92A06f9e2aB34cbF837D79501f51cacc95A9cb2"
        }
    }

Request Response
~~~~~~~~
Initially you'll get an immediate feedback like the one below if your API request is successfull.

.. raw:: html

    <div>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">PartnerRequestID:</span> [string] Client id.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">CollectionRequestID:</span> [string] Unique collection request id.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResponseCode:</span> [number] Response code.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResponseDescription:</span> [string] Response code description.</p>
    </div>

.. code-block:: javascript
      
      {
         "PartnerRequestID": "66386452d8d95fb8b8870859",
         "CollectionRequestID": "e3e73daf-e257-4f90-9077-291471ec6157",
         "ResponseCode": 1,
         "ResponseDescription": "Collection request accepted for processing"
      }

Later after successful execution, your webhook url will be called and you'll get full overview of the collection request initiated. Check :doc:`webhook` for more information

2. GET /collections/query_transaction/{collectionRequestId}
~~~~~~~~~

Overview
~~~~~~~
This API is used to query the status of a collection request.

GET Request URL 
~~~~~~~~~
.. raw:: html

      <p style="color: red;">https://sandbox.hurupay.com/v1/collections/query_transaction/{collectionRequestId}</p>

Request Headers
~~~~~~~~~

.. code-block:: javascript

    headers: {
        Authorization: `Bearer ${your-key}`,
        "Content-Type": "application/json"
        "X-Target-Environment": "your environment"
    }

Response
~~~~~~~~
You'll get an immediate feedback like the one below if your API request is successfull.

.. raw:: html

    <div>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResultCode:</span> [number] Collection request code status.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">PartnerRequestID:</span> [string] Client id.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">CollectionRequestID:</span> [string] Collection request Id.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResultDescription:</span> [string] Status code result description.</p>
    </div>

.. code-block:: javascript
      
      {
         "ResultCode": 1,
         "PartnerRequestID": "66386452d8d95fb8b8870859",
         "CollectionRequestID": "7cf7a5c5-7c69-4ef4-8aa1-2e3371a97a47",
         "ResultDescription": "The service request has been proccesed successfully"
      }

Result Code Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~
+-------------+------------------------------------------------+
| Status Code | Message                                        | 
+=============+================================================+
| 0           | The collection transaction was successfull     | 
+-------------+------------------------------------------------+
| 1032        | Transaction process was cancelled.             | 
+-------------+------------------------------------------------+
| 1           | The collection transaction failed              | 
+-------------+------------------------------------------------+



.. autosummary::
   :toctree: generated

   lumache
