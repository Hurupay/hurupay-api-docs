Exchange Rates
==============


Overview
^^^^^^^^
The exchange rate API service allows clients to calculate the amount of digital asset tokens or fiat amount that will be deposited to user wallet address account or mobile money respectively in realtime.

Base URL
^^^^^^^^
The URL for the On demand API is https://sandbox.hurupay.com/v1

Authentication
^^^^^^^^
The exchange API uses client's apikey **(sandbox key or production key)**. Include your `client key` and `x-target-environment` in each request headers to the API.

.. code-block:: javascript

    headers: {
        
        "Content-Type": "application/json",
        Authorization: `Bearer ${your-api-key}`,
    }

.. note::
    
    Base currency is USD

    Below is a list of accepted/supported **to** currency for this API service:

    - KES
    - GHS
    - TZS
    - XAF

Endpoints
^^^^^^^^^

GET /exchange/transfer_rate?from=${fromCurrency}&to={toCurrency}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Get the withdrawal rate for a specific currency.

Example Request 

.. code-block:: console

    GET Request https://sandbox.hurupay.com/v1/exchange/transfer_rate?from=USD&to=KES


Example Response:

.. code-block:: javascript

    {
        "status": "success",
        "updated_date": "2024-08-13T17:19:33.708Z",
        "baseCurrencyCode": "USD",
        "amount": 1,
        "rates": {
            "KES": {
                "currencyName": "Kenyan shilling",
                "rate": "127.00"
            }
        }
    }

.. autosummary::
   :toctree: generated

   lumache