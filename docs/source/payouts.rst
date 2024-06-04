Payouts
=======

Mobile Money
------------

Overview
^^^^^^^^
The API service facilitates seamless integration of various mobile money wallets and mobile services across listed countries. It supports notable providers such as Safaricom and MTN, enabling clients to streamline the process of converting stable coins digital assets into equivalent fiat amount. This service is designed to assist with off-ramping supported stable coins(**cUSD & USDT**).

Base URL
^^^^^^^^
The URL for collections API is https://api.hurupay.com/v1

Authentication
^^^^^^^^^^^^^^
The collection API uses client's apikey **(sandbox key or production key)**. Include your `client key` and `x-target-environment` in each request headers to the API.

.. note::

      X-Target-Environment value should match your private key:

      * For sandbox key, use `sandbox` as X-Target-Environment
      * For production key, use `production` as X-Target-Environment

Endpoints
^^^^^^^^

1. POST /payouts/mobile/initialize_transaction
~~~~~~~~~

POST Request URL 
~~~~~~~~~
.. raw:: html

      <p style="color: red;">https://api.hurupay.com/v1/payouts/mobile/initialize_transaction</p>

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
        "TransactionHash":"0x697fbcd3bae946ae2c6c887899adc6e62addae3bd2ee5eb6203374d5ee1e19d8",
        "PhoneNumber":"254720000000",
        "EmailAddress":"xyz@example.com",
        "ISOCurrency":"GHS"
    }

Request Response
~~~~~~~~
Initially you'll get an immediate feedback like the one below if your API request is successfull.

.. raw:: html

    <div>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">PartnerRequestID:</span> [string] Client id.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">PayoutRequestID:</span> [string] Unique collection request id.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResponseCode:</span> [number] Response code.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResponseDescription:</span> [string] Response code description.</p>
    </div>

.. code-block:: javascript
      
      {
         "PartnerRequestID": "66386452d8d95fb8b8870859",
         "PayoutRequestID": "e3e73daf-e257-4f90-9077-291471ec6157",
         "ResponseCode": 1,
         "ResponseDescription": "Payout request accepted for processing"
      }

2. GET /payouts/mobile/query_transaction/{payoutRequestId}
~~~~~~~~~

Overview
~~~~~~~
This API is used to query the status of a payout request.

The status of the payout will be on pending status (**ResultCode:0**) until the B2C transaction is complete.

GET Request URL 
~~~~~~~~~~~~~~~
.. raw:: html

      <p style="color: red;">https://api.hurupay.com/v1/payouts/query_transaction/{payoutRequestId}</p>

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
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">PayoutRequestID:</span> [string] Collection request Id.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResultDescription:</span> [string] Status code result description.</p>
    </div>

.. code-block:: javascript
      
      {
         "ResultCode": 1,
         "PartnerRequestID": "66386452d8d95fb8b8870859",
         "PayoutRequestID": "7cf7a5c5-7c69-4ef4-8aa1-2e3371a97a47",
         "ResultDescription": "The service request has been proccesed successfully"
      }

Result Code Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~
+-------------+------------------------------------------------+
| Status Code | Message                                        | 
+=============+================================================+
| 0           | The payout request transaction is pending      | 
+-------------+------------------------------------------------+
| 1032        | Transaction process was cancelled.             | 
+-------------+------------------------------------------------+
| 1           | The collection transaction was successfull     | 
+-------------+------------------------------------------------+