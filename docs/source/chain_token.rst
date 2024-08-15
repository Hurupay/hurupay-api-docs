On/Off Ramp Chains & Tokens
===========================

Overview
^^^^^^^^
This API endpoint provides a comprehensive list of all supported blockchain networks and their respective tokens. It allows you to quickly identify which chains and tokens are available for on-ramp and off-ramp transactions via Hurupay.

GET Request URL
^^^^^^^^^^^^^^^
To retrieve the list of supported chains and tokens, use the following endpoint:

.. code-block:: console

    GET https://sandbox.hurupay.com/v1/chain/supported

Request Headers
~~~~~~~~~~~~~~~

Include your API key in the request headers to authenticate the request.

.. code-block:: javascript

    headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${your-api-key}`
    }

Response
~~~~~~~~

Upon a successful request, you will receive a response containing the list of supported chains and their corresponding tokens.

.. code-block:: javascript

    {
        "success": true,
        "message": "All supported chains and their respective tokens fetched successfully",
        "data": [
            {
                "chain": {
                    "STELLAR": [
                        "USDC"
                    ]
                }
            },
            {
                "chain": {
                    "CELO": [
                        "cUSD"
                    ]
                }
            }
        ]
    }
