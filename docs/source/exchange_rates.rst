Exchange Rates
==============


Overview
^^^^^^^^
The exchange rate API service allows clients to calculate the amount of digital asset tokens or fiat amount that will be deposited to user wallet address account or mobile money respectively in realtime.

Base URL
^^^^^^^^
The URL for the On demand API is https://api.hurupay.com/exchange/v1

Authentication
^^^^^^^^
The exchange API uses client's apikey **(sandbox key or production key)**. Include your `client key` and `x-target-environment` in each request headers to the API.

.. code-block:: javascript

    headers: {
        Authorization: `Bearer ${your-key}`,
        "Content-Type": "application/json"
        "X-Target-Environment": "your environment"
    }

.. note::

    Below is a list of accepted/supported ISO Currencies for this API service:

    - KES
    - GHS
    - UGX
    - NGN
    - TZS
    - RWF

Endpoints
^^^^^^^^

GET /deposit_rate?to={ISOCurrency}
~~~~~~~~~
Get the deposit rate for a specific currency.

Example Request

.. code-block:: console
    
    GET Request https://api.hurupay.com/exchange/deposit_rate?to=KES

Example Response:

.. code-block:: javascript
        
    {
        "status": "success",
        "updated_date": "2024-05-28T21:00:01.546Z",
        "baseCurrencyCode": "USD",
        "amount": 1,
        "baseCurrencyName": "United States Dollar",
        "rates": {
            "KES": {
                "currencyName": "Kenyan shilling",
                "rate": "136.98"
            }
        }
    }

GET /withdrawal_rate?to={ISOCurrency}
~~~~~~~~~~
Get the withdrawal rate for a specific currency.

Example Request 

.. code-block:: console

    GET Request https://api.hurupay.com/exchange/withdrawal_rate?to=KES


Example Response:

.. code-block:: javascript

    {
        "status": "success",
        "updatedAt": "2024-05-28T21:00:01.546Z",
        "baseCurrencyCode": "USD",
        "amount": 1,
        "baseCurrencyName": "United States Dollar",
        "rates": {
            "KES": {
                "currencyName": "Kenyan shilling",
                "rate": "126.98"
            }
        }
    }

.. autosummary::
   :toctree: generated

   lumache