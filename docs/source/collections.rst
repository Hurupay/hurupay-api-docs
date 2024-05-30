Collections
===========

.. _mobile_money:

Mobile Money
------------

Overview
^^^^^^^^
The API service facilitates seamless integration of various mobile money wallets and mobile services across listed countries. It supports notable providers such as Safaricom and MTN, enabling clients to streamline the process of converting local currencies into equivalent stablecoin dollars. This service is designed to assist with on-ramping, ensuring a smooth transition into the digital currency ecosystem.

.. note::
   The mobile money service is currently available in:

   * `Kenya (Safaricom M-pesa mobile money service)`,
   * `Ghana (MTM momo mobile money service)`,
   * `Nigeria (MTM momo mobile money service)`,
   * `Uganda (MTM momo mobile money service)`, 
   * `Tanzania (MTM momo mobile money service)`, 
   * `Rwanda (MTM momo mobile money service).`

Base URL
^^^^^^^^
The URL for collections API is https://api.hurupay.com

Authentication
^^^^^^^^^^^^^^
The collection API uses client's apikey **(sandbox key or production key)**. Include your `client key` and `x-target-environment` in each request headers to the API.

.. note::

      X-Target-Environment value should match your private key:

      * For sandbox key, use `sandbox` as X-Target-Environment
      * For production key, use `production` as X-Target-Environment

Endpoints
^^^^^^^^

1. POST /collections/mobile/initialize_transaction
~~~~~~~~~

Overview
~~~~~~~
This endpoint is used to facilitate digital asset or tokens deposit to user's wallet address. The phone number provided in the request body will receive a request to pay prompt, If the user completes the request succesfully, Hurupay will credit the user's `Wallet address` with respective digital asset amount both provided in the request body. Token amount is according to Hurupay's :doc:`exchange_rates` API

POST Request URL 
~~~~~~~~~
.. raw:: html

      <p style="color: red;">https://api.hurupay.com/collections/mobile/initialize_transaction</p>

Request Headers
~~~~~~~~~

.. code-block:: javascript

    headers: {
        Authorization: `Bearer ${your-key}`,
        "Content-Type": "application/json"
        "X-Target-Environment": "your environment"
    }

Request Body
~~~~~~~~~

.. code-block:: javascript

   {
    "PhoneNumber":"254704407239",
    "EmailAddress":"xyz@example.com",
    "TransactionMethod":"MobileMoney",
    "Amount":"10",
    "ISOCurrency":"KES",
    "WalletAddress":"0x67279306F1e188FD6bEE167203E1bE49661755Bf",
    "DigitalAsset":"cUSD"
   }

Response
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

Later after successful execution, your webhook url will be called and you'll get full overview of the collection request initiated. Check :doc:`webhooks` for more information

2. GET /collections/query_transaction/{collectionRequestId}
~~~~~~~~~

Overview
~~~~~~~
This API is used to query the status of a collection request.

GET Request URL 
~~~~~~~~~
.. raw:: html

      <p style="color: red;">https://api.hurupay.com/collections/query_transaction/{collectionRequestId}</p>

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
Initially you'll get an immediate feedback like the one below if your API request is successfull.

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
| 0           | The collection transaction is pending          | 
+-------------+------------------------------------------------+
| 1032        | Transaction process was cancelled.             | 
+-------------+------------------------------------------------+
| 1           | The collection transaction was successfull     | 
+-------------+------------------------------------------------+



.. autosummary::
   :toctree: generated

   lumache
