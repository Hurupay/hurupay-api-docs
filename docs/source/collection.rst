Mobile Money Collections (On Ramp)
=================================

Overview
^^^^^^^^
The **Hurupay API** service enables seamless integration with various mobile money wallets and services across supported countries. It connects with top providers like **Safaricom (MPESA)**, **Airtel**, **MTN**, and **TIGO**, facilitating the conversion of local currencies into stablecoins. This service is essential for clients looking to onboard into the digital currency ecosystem efficiently.

.. note::
   The mobile money service is currently available in:

   * **Kenya (MPESA)**
   * **Ghana (MTN, VODAFONE, TIGO, AIRTEL)**
   * **Tanzania (MTN, VODACOM, TIGO, AIRTEL)**

Base URL
^^^^^^^^
The BASE URL for the API is:

`https://sandbox.hurupay.com/v1`

Authentication
^^^^^^^^^^^^^^
To access the collection API, use your partner's API key (either sandbox or production). Include this key in the request headers for authentication.

Endpoints
^^^^^^^^^

1. POST /collections/mobile/initialize_transaction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Overview
~~~~~~~~
This endpoint is used to deposit digital assets into a user's wallet. The user will receive a request-to-pay prompt on their mobile device. Upon successful payment, Hurupay will credit the specified wallet address with the corresponding digital assets. The token amount is calculated using Hurupay's :doc:`exchange_rates` API Service.

POST Request URL 
~~~~~~~~~~~~~~~~~
.. code-block:: console

    GET https://sandbox.hurupay.com/v1/collections/mobile/initialize_transaction

Request Headers
~~~~~~~~~~~~~~~

.. code-block:: javascript

    headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${Your-Api-Key}`,
    }

Request Body
~~~~~~~~~~~~

.. code-block:: javascript

   {
        "collection": {
            "customerName": "John Doe",
            "customerEmail": "johndoe@gmail.com",
            "phoneNumber": "+2547XXXXXX",
            "countryCode": "KE",
            "network": "MPESA",
            "amount": 1
        },
        "transfer": {
            "digitalNetwork": "CELO",
            "digitalAsset": "cUSD",
            "walletAddress": "0xD92A06f9e2aB34cbF837D79501f51cacc95A9cb2"
        }
    }

Request Response
~~~~~~~~~~~~~~~~
Initially, you'll get an immediate feedback like the one below if your API request is successful.

.. raw:: html

    <div>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">PartnerRequestID:</span> [string] Client ID.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">CollectionRequestID:</span> [string] Unique collection request ID.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResponseCode:</span> [number] Response code.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResponseDescription:</span> [string] Response description.</p>
    </div>

.. code-block:: javascript
      
    {
        "success": true,
        "message": "Collection request accepted for processing",
        "data": {
            "PartnerRequestID": "66bc4d75d8deec854010a9a9",
            "CollectionRequestID": "cd4d492f-9017-4c4a-85c7-76607ce7fe68",
            "ResponseCode": 1,
            "ResponseDescription": "Collection request accepted for processing"
        }
    }

Later, after successful execution, your webhook URL will be called and you'll get a full overview of the collection request initiated. Check :doc:`webhook` for more information.

2. GET /collections/query_transaction/{collectionRequestId}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Overview
~~~~~~~~
This API is used to query the status of a collection request.

GET Request URL 
~~~~~~~~~~~~~~~
.. code-block:: console

    GET https://sandbox.hurupay.com/v1/collections/query_transaction/{collectionRequestId}

Request Headers
~~~~~~~~~~~~~~~

.. code-block:: javascript

    headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${your-key}`,
    }

Response
~~~~~~~~

.. code-block:: javascript

    {
        "success": true,
        "message": "Collection transaction retrieved successfully",
        "data": {
            "ResponseCode": 0,
            "ResponseCodeDescription": "Service request completed",
            "ResultCode": 0,
            "ResultCodeDescription": "onramp transaction was completed successfuly",
            "CollectionRequestID": "cd4d492f-9017-4c4a-85c7-76607ce7fe68"
        }
    }


Result Code Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~
+-------------+-------------------------------------------------------+
| Status Code | Message                                               | 
+=============+=======================================================+
| 0           | The offramp request is completed successfully         | 
+-------------+-------------------------------------------------------+
+-------------+-------------------------------------------------------+
| 1           | The off ramp transaction was unsuccessfull            | 
+-------------+-------------------------------------------------------+

Response Code Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~
+-------------+-------------------------------------------------------+
| Status Code | Message                                               | 
+=============+=======================================================+
| 0           | The transaction was completed (failed or successful)  | 
+-------------+-------------------------------------------------------+ 
+-------------+-------------------------------------------------------+
| 1           | The transaction is not complete yet (pending)         | 
+-------------+-------------------------------------------------------+

.. autosummary::
   :toctree: generated

   lumache
