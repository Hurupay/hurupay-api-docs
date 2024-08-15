Partner Integration Guide
=========================

Welcome to the Partner API service! This documentation will guide you through the steps to integrate your system as a partner with Hurupay, enabling seamless interaction with our services.

.. _partner:

Base URL
--------
The base URL for accessing the Hurupay Partner API in the sandbox environment is:

**BASE URL:** `https://sandbox.hurupay.com/v1`

Create a Partner Account
-------------------------

To get started, you'll need to create a partner account. This is your gateway to accessing all the features of the Hurupay API.

**Endpoint**

**POST Request URL:** 

.. code-block:: console

      POST https://sandbox.hurupay.com/v1/partner

**Request Body**

Supply the following JSON object with your details:

.. code-block:: javascript

    {
      "companyName":"XYZ Limited",
      "firstName":"John",
      "lastName":"Doe",
      "email":"johndoe@gmail.com",
      "phoneNumber":"+2547XXXXXXXX",
      "countryCode":"KE"
    }

**Successful Response**

Upon successful creation, you'll receive the following response:

.. code-block:: javascript
      
    {
      "success": true,
      "message": "Partner created successfully",
      "data": {
        "_id": "66b9cf56c66c6047aebb8b0d",
        "companyName": "XYZ Limited",
        "firstName": "John",
        "lastName": "Doe",
        "email": "johndoe@gmail.com",
        "phoneNumber": "+2547XXXXXXXX",
        "countryCode": "KE"
      }
    }

Partner Authentication
-----------------------

Once you've created your partner account, you'll need to authenticate to gain access to secure endpoints.

**Sign-In Authentication**

This process sends a magic hash to your registered email, which you'll use to authorize your account.

**POST Request URL:**

.. code-block:: console

      POST https://sandbox.hurupay.com/v1/auth/login

**Request Body**

Include your registered email address:

.. code-block:: javascript

    {
      "email":"johndoe@gmail.com"
    }

**Successful Response**

If successful, you'll receive a confirmation message:

.. code-block:: javascript
      
    {
      "success": true,
      "message": "Magic hash for authorization has been sent to your email",
      "data": {}
    } 

**Authorize Partner Account**

Use the magic hash from your email to complete the authorization and retrieve your access tokens.

**GET Request URL:**

.. code-block:: console

      GET https://sandbox.hurupay.com/v1/auth/verify?hash={magichash}

**Successful Response**

A successful authorization will return your partner ID and tokens:

.. code-block:: javascript
      
    {
      "success": true,
      "message": "Authorization successful",
      "data": {
        "partnerId": "66b9cf56c66c6047aebb8b0d",
        "access_token": "your_access_token_here",
        "refresh_token": "your_refresh_token_here"
      }
    }

Generate Your API Key
---------------------

With your access token in hand, you can now generate your API key, which is essential for making secure API requests.

**GET Request URL:**

.. code-block:: console

      GET https://sandbox.hurupay.com/v1/auth/api_key?token={accessToken}

**Successful Response**

Your API key will be returned in the following format:

.. code-block:: javascript
      
    {
      "success": true,
      "message": "API Key generated successfully",
      "data": {
        "apiKey": {
          "partnerId": "66b9cf56c66c6047aebb8b0d",
          "apiKey": "your_api_key_here"
        }
      }
    }

Retrieve Partner Information
----------------------------

You can fetch details about your partner integrator account at any time using the endpoint below.

**GET Request URL:**

.. code-block:: console

      GET https://sandbox.hurupay.com/v1/partner?token={accessToken}

**Successful Response**

If the request is successful, you'll receive the following response:

.. code-block:: javascript

    {
      "success": true,
      "message": "Partner record successfully retrieved",
      "data": {
        "_id": "66bc4d75d8deec854010a9a9",
        "companyName": "XYZ Company",
        "firstName": "John",
        "lastName": "Doe",
        "email": "johndoe@gmail.com",
        "phoneNumber": "+2547XXXXXXX",
        "countryCode": "KE"
      }
    }