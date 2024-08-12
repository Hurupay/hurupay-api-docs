Partner
=======
This API service will help you create a partner integrator 

.. _partner:

Base URL
--------
BASE URL is https://sandbox.hurupay.com/v1

Create Partner
--------------

POST Request URL 

.. raw:: html

      <p style="color: red;">https://sandbox.hurupay.com/v1/partner</p>

Request Body

.. code-block:: javascript

   {
    "companyName":"XYZ Limited",
    "firstName":"John",
    "lastName":"Doe",
    "email":"johndoe@gmail.com",
    "phoneNumber":"+2547XXXXXXXX",
    "countryCode":"KE"
    }

Successful Request Response

.. code-block:: javascript
      
      {
        "success": true,
        "message": "partner created successfully",
        "data": {
            "_id": "66b9cf56c66c6047aebb8b0d",
            "companyName": "XYZ Limited",
            "firstName": "John",
            "lastName": "Doe",
            "email": "johndoe@gmail.com",
            "phoneNumber": "+2547XXXXXXXX",
            "countryCode": "KE",
            }
       } 

Partner Authentication
----------------------

Sign in authentication
^^^^^^^^^^

After successfully creating partner account you need to authorize your account in order to get access_token and refresh_token. 
This API will send you a magic hash to your email that you will you use to authorize your account.

POST Request URL 

.. raw:: html

      <p style="color: red;">https://sandbox.hurupay.com/v1/auth/login</p>

Request Body

.. code-block:: javascript

   {
    "email":"johndoe@gmail.com",
    }

Successful Request Response

.. code-block:: javascript
      
      {
        "success": true,
        "message": "magic hash for authorization has has been sent to your email",
        "data": {}
      } 

Authorize partner account
^^^^^^^^^^^^^^^^^^^^^^^^

Use the magic hash received in your email to authorize your partner account in order to get access_token for your next action

GET Request URL 

.. raw:: html

      <p style="color: red;">https://sandbox.hurupay.com/v1/auth/verify?hash={magichash}</p>

Successful Request Response

.. code-block:: javascript
      
      {
        "success": true,
        "message": "authorization successful",
        "data": {
            "partnerId": "66b9cf56c66c6047aebb8b0d",
            "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2NmI5Y2Y1NmM2NmM2MDQ3YWViYjhiMGQiLCJjb21wYW55TmFtZSI6Ikh1cnVwYXkgQ29tcGFueSBMaW1pdGVkIiwiZmlyc3ROYW1lIjoiTWF4d2VsIiwibGFzdE5hbWUiOiJPY2hpZW5nIiwiZW1haWwiOiJlbmcubWF4d2VsLm9jaGllbmdAZ21haWwuY29tIiwicGhvbmVOdW1iZXIiOiIrMjU0NzA0NDA3MjM5IiwiY291bnRyeUNvZGUiOiJLRSIsImlzQWRtaW4iOmZhbHNlLCJjcmVhdGVkQXQiOiIyMDI0LTA4LTEyVDA5OjAxOjEwLjQ4MloiLCJ1cGRhdGVkQXQiOiIyMDI0LTA4LTEyVDA5OjAxOjEwLjQ4MloiLCJfX3YiOjAsImlhdCI6MTcyMzQ1NDY2MywiZXhwIjoxNzIzNTQxMDYzfQ.ayVp3LjzzCqN5j93mWH6td6wN1ObaTkEhmWCQxpgpbu-Oln_uVuBmiEo7S6O4E6wbZtB-zTSt1gicUE8dZtfQTxhD8t_-zG5yLG-76KgMv-wPwmTIkN5Agug17563RS-czFVkJAgErHO-u66CJAD-RvI3VkHNSO3XDh02Ac3P8ReWQMdUdLg_cY_y3aXbivcT2NinAhRp1YJ6-JAgHjUGxgguIHDMZ_WpAQ6fJN-oAbHyFXJb-aiVtML115fto0tDOXPtCObMQGxcfTSdds0xqxcRipP7Q2cnEULM49sNyj1BG-1mn_TgPkjgeRwhDylugRDzuXAk46ku0BOSfMZCQ",
            "refreshToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzZXNzaW9uIjoiNjZiOWQ0YzdjNjZjNjA0N2FlYmI4YjE1IiwiaWF0IjoxNzIzNDU0NjYzLCJleHAiOjE3MjM0NTQ3MjN9.WkZqXLAzPemm4o44JEEhZ9t8sMt3UAvToiooXyjIF-e6Ip1gA1Sg1VZBU1101foLyiEWO1epDRO-XqKaImxcSCcZ_igaqT8cVOtu3EFFh1o2DrtTnt4aGuKvicC3E-W8irLfnGMAY9Qp0b7gN0Kt3UqyHjMB-YidG6C_xUyyD69tW0k2c2wO_OQXkCSwtT-O6cE986Iy6HFMyMcst_8IHQhEgsgloBz2mC-oVRRQ8Urujb_YLCCOJmI_9xapsglk_GJnguRbjGXZXRLPnR_5cuNdTcSliVIYZEQXpLHvbqKV8FeUXf96enIn0Dj5L3-gJfAh_EkXVMLLPVxIEHocRQ"
            }
        } 

Generate Partner API Key
^^^^^^^^^^^^^^^^^^^^^^^^

After successfully generating your access token, use it to generate your API KEY that you'll use in the other sections of the API such as collections, payouts and webhhoks.

GET Request URL 

.. raw:: html

      <p style="color: red;">https://sandbox.hurupay.com/v1/auth/api_key?token={accessToken}</p>

Successful Request Response

.. code-block:: javascript
      
      {
        "success": true,
        "message": "Api-Key generated successfully",
        "data": {
            "apiKey": {
                "partnerId": "66b9cf56c66c6047aebb8b0d",
                "apiKey": "hp_sk_314hhafycbilipfkyvmptdpfdfrm54rthnm27jpi",
            }
        }
      } 