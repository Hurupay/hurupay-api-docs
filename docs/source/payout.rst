Mobile Money Payouts (Off Ramp)
===============================

Overview
^^^^^^^^
Unlock seamless conversion of digital assets into local currency with **Hurupay’s Mobile Money Payouts**. This API service integrates effortlessly with various mobile money wallets and services across multiple countries, supporting major providers like **Safaricom** and **MTN**. Whether you're off-ramping **cUSD** or **USDT**, our platform ensures a smooth transition from stable coins to fiat currency.

Base URL
^^^^^^^^
For all payout requests, use the following URL:

.. code-block:: text

    https://sandbox.hurupay.com/v1

Authentication
^^^^^^^^^^^^^^
To access the payout API, include your partner’s API key (sandbox or production) in the request headers. This key authenticates your requests, ensuring secure communication with Hurupay's servers.

Endpoints
^^^^^^^^^

1. POST /payouts/mobile/initialize_transaction/request
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Initiate the off-ramp process by generating a wallet address where you’ll send the tokens. This step provides a transaction hash required for subsequent operations.

**POST Request URL**

.. code-block:: console

    POST https://sandbox.hurupay.com/v1/payouts/mobile/initialize_transaction/request

**Request Headers**

.. code-block:: javascript

    headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${your-api-key}`,
    }

**Request Body**

.. code-block:: javascript

    {
        "sendingAddress": "0xD92A06f9e2aB34cbF837D79501f51cacc95A9cb2",
        "amountSending": "1",
        "network": "CELO",
        "token": "cUSD"
    }

**Successful Response**

Upon a successful request, you’ll receive the following response with an escrow address and a unique payout request ID for the next steps:

.. code-block:: javascript

    {
        "success": true,
        "message": "Payout request created",
        "data": {
            "payoutRequestId": "0e519064-322b-4bdd-a1af-1d3ece747678",
            "escrowAddress": "0x67279306F1e188FD6bEE167203E1bE49661755Bf"
        }
    }

2. POST /payouts/mobile/initialize_transaction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Finalize the off-ramp process by providing the transaction hash and payout request ID obtained from the previous step.

**POST Request URL**

.. code-block:: console

    POST https://sandbox.hurupay.com/v1/payouts/mobile/initialize_transaction

**Request Headers**

.. code-block:: javascript

    headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${your-api-key}`,
    }

**Request Body**

.. code-block:: javascript

    {
        "collection": {
            "transactionHash": "20aa90584c95e7fd67a210bee3a34f7dfb7fbf0c3efa38d0b0b7838cfd145bef",
            "payoutRequestId": "9d2681ab-440a-403d-bb2b-79123ee1ace9",
            "network": "CELO",
            "token": "cUSD"
        },
        "transfer": {
            "customerName": "John Doe",
            "phoneNumber": "+2547XXXXXXX",
            "countryCode": "KE",
            "network": "MPESA"
        }
    }

**Immediate Response**

You will receive an immediate response confirming that the payout request was accepted for processing. For the full details of the payout transaction, refer to the **webhooks** section.

.. raw:: html

    <div>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">PartnerRequestID:</span> [string] Client ID.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">PayoutRequestID:</span> [string] Unique collection request ID.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResponseCode:</span> [number] Response code.</p>
      <p><span style="color: red; border: 1px solid #000; padding: 5px;">ResponseDescription:</span> [string] Response code description.</p>
    </div>

.. code-block:: javascript

    {
        "success": true,
        "message": "Payout request accepted for processing",
        "data": {
            "ResultCode": 1,
            "PartnerRequestID": "66bc4d75d8deec854010a9a9",
            "ResultDescription": "Success. Process accepted for processing"
        }
    }

3. GET /payouts/mobile/query_transaction/{payoutRequestId}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Use this endpoint to query the status of a payout request. The status will remain **pending** (ResultCode: 0) until the B2C transaction is complete.

**GET Request URL**

.. code-block:: console

    GET https://sandbox.hurupay.com/v1/payouts/query_transaction/{payoutRequestId}

**Request Headers**

.. code-block:: javascript

    headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${your-api-key}`
    }

**Response**

If successful, you'll receive a response similar to the one below, indicating the transaction status.

.. code-block:: javascript

    {
        "success": true,
        "message": "Payout transaction received",
        "data": {
            "ResponseCode": 0,
            "ResponseCodeDescription": "Payout transaction process completed",
            "ResultCode": 0,
            "ResultCodeDescription": "Offramp transaction was completed successfully",
            "PartnerRequestID": "66bc4d75d8deec854010a9a9",
            "PayoutRequestID": "0e519064-322b-4bdd-a1af-1d3ece747678"
        }
    }

Result Code Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~
Understanding the meaning of different status codes:

+-------------+-------------------------------------------------------+
| Status Code | Message                                               | 
+=============+=======================================================+
| 0           | The off-ramp request is completed successfully        | 
+-------------+-------------------------------------------------------+
| 1           | The off-ramp transaction was unsuccessful             | 
+-------------+-------------------------------------------------------+

Response Code Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~~~
Detailed explanation of response codes:

+-------------+-------------------------------------------------------+
| Status Code | Message                                               | 
+=============+=======================================================+
| 0           | The transaction was completed (failed or successful)  | 
+-------------+-------------------------------------------------------+ 
| 1           | The transaction is not complete yet (pending)         | 
+-------------+-------------------------------------------------------+
