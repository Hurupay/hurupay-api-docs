Webhooks
========

Webhooks: Real-time Transaction Updates
---------------------------------------

Webhooks Overview
^^^^^^^^^^^^^^^^^
**Imagine** knowing the status of your transactions the moment they happen—no refreshing, no waiting. With **Hurupay's Webhooks**, you can create a dynamic notification system that keeps you in the loop on all your **Collection** and **Payout API** activities.

When the status of your API calls changes, Hurupay’s resource server **immediately** notifies your server via webhooks. This status change, known as an event, triggers a notification that you can handle through a POST endpoint.

A webhook URL is essentially a **POST endpoint** that your server listens to for updates. It must be able to parse a JSON request and respond with a status OK to acknowledge receipt.

For both **On Ramp** and **Off Ramp** transactions, it’s essential to have webhooks set up to capture the final status—whether success or failure. **And here’s the best part:** you can configure more than one webhook URL, tailoring the experience to your needs.

.. code-block:: javascript
    :caption: Express.js Example of a Webhook Endpoint to Handle Collection Updates

    router.post("/collection/webhook/url", function(req, res) {
        // Retrieve the request's body
        const event = req.body;
        console.log(event)
        res.status(200).send('OK');
    });

Partner Webhooks
----------------

Ready to set up your webhooks? Let’s dive in:

Request Headers
~~~~~~~~~~~~~~~
Your webhook interactions require the following headers:

.. code-block:: javascript

    headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${your-api-key}`
    }

Create Webhook
~~~~~~~~~~~~~~
Start by creating a new webhook:

.. code-block:: console

    POST https://sandbox.hurupay.com/v1/webhook

**Request Body**

Here’s how your request body should look:

.. code-block:: javascript

    {
        "url":"https://hurupay.com/v1/webhooks/global_payout",
        "type":"collections"
    }

**Request Response**

Upon a successful creation, you’ll receive the following response:

.. code-block:: javascript
    
    {
        "success": true,
        "message": "Webhook created successfully",
        "data": {
            "partnerId": "66bbfc205a5ec9406fdd2d5a",
            "url": "https://hurupay.com/v1/webhooks/global_payout",
            "type": "collections",
            "publicKey": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAt/RD+L0L5T1rK212Yv89\nhvbES7DEwgMNvj22xlEij/7Orl6CgEQDuXisjHFqiIWe05tpR6AMWlRrggb9O+kw\nZsMrHWOp9SNcNIsR8rka5fqVSbYE8mXqtw4f4MUbB8AnRQRYIyXvlxMT1eWlXTJo\nokHsiYanA2zx3uXkDs/Ia+8B2/xKvK3UUbVa2I/b+MIWk7y02wHGFE9Zu4J98+uA\nJluS9GUEyGRtxyb+muoApGlxV9j0Qw8zhr1VPb5sjOzGKwAYfiNGNZoE59BFYM9E\nM7PfO+JWSGc6RHwNSsLxVKoj42zv6LQ2nhJ15YMuVKVD5Hb57oR6hQantzZaA3gE\n5wIDAQAB\n-----END PUBLIC KEY-----\n"
        }
    }

List All Webhooks
~~~~~~~~~~~~~~~~~
Curious to see all your webhooks? Use this command:

.. code-block:: console

    GET https://sandbox.hurupay.com/v1/webhook

**Request Response**

Here’s the response showing your existing webhooks:

.. code-block:: javascript

    {
    "success": true,
    "message": "webhooks fetched successfully",
    "data": [
        {
            "_id": "670508254bf89d3d77025460",
            "partnerId": "66bbfc205a5ec9406fdd2d5a",
            "url": "https://hurupay.com/v1/webhooks/global_payout",
            "type": "collections",
            "publicKey": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAt/RD+L0L5T1rK212Yv89\nhvbES7DEwgMNvj22xlEij/7Orl6CgEQDuXisjHFqiIWe05tpR6AMWlRrggb9O+kw\nZsMrHWOp9SNcNIsR8rka5fqVSbYE8mXqtw4f4MUbB8AnRQRYIyXvlxMT1eWlXTJo\nokHsiYanA2zx3uXkDs/Ia+8B2/xKvK3UUbVa2I/b+MIWk7y02wHGFE9Zu4J98+uA\nJluS9GUEyGRtxyb+muoApGlxV9j0Qw8zhr1VPb5sjOzGKwAYfiNGNZoE59BFYM9E\nM7PfO+JWSGc6RHwNSsLxVKoj42zv6LQ2nhJ15YMuVKVD5Hb57oR6hQantzZaA3gE\n5wIDAQAB\n-----END PUBLIC KEY-----\n",
            "status": "active"
        }
    ]
}

Find Webhook by ID
~~~~~~~~~~~~~~~~~~
Looking for a specific webhook? Here's how:

.. code-block:: console

    GET https://sandbox.hurupay.com/v1/webhook/{webhookId}

**Request Response**

Retrieve details about the specified webhook:

.. code-block:: javascript

    {
        "success": true,
        "message": "webhook fetched successfully",
        "data": {
            "_id": "670508254bf89d3d77025460",
            "partnerId": "66bbfc205a5ec9406fdd2d5a",
            "url": "https://hurupay.com/v1/webhooks/global_payout",
            "type": "collections",
            "publicKey": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAt/RD+L0L5T1rK212Yv89\nhvbES7DEwgMNvj22xlEij/7Orl6CgEQDuXisjHFqiIWe05tpR6AMWlRrggb9O+kw\nZsMrHWOp9SNcNIsR8rka5fqVSbYE8mXqtw4f4MUbB8AnRQRYIyXvlxMT1eWlXTJo\nokHsiYanA2zx3uXkDs/Ia+8B2/xKvK3UUbVa2I/b+MIWk7y02wHGFE9Zu4J98+uA\nJluS9GUEyGRtxyb+muoApGlxV9j0Qw8zhr1VPb5sjOzGKwAYfiNGNZoE59BFYM9E\nM7PfO+JWSGc6RHwNSsLxVKoj42zv6LQ2nhJ15YMuVKVD5Hb57oR6hQantzZaA3gE\n5wIDAQAB\n-----END PUBLIC KEY-----\n",
            "status": "active"
            }
    }

Enable or Disable Webhook
~~~~~~~~~~~~~~~~~~~~~~~~~
Need to toggle a webhook’s status? Here’s how:

.. code-block:: console

    PUT https://sandbox.hurupay.com/v1/webhook/{webhookId}

**Request Body**

Set the status to "active" or "disabled":

.. code-block:: javascript

    {
        "status":"active"
    }

**Request Response**

Confirmation of the status change:

.. code-block:: javascript
    
    {
        "success": true,
        "message": "webhook fetched successfully",
        "data": {
                "_id": "670508254bf89d3d77025460",
                "partnerId": "66bbfc205a5ec9406fdd2d5a",
                "url": "https://hurupay.com/v1/webhooks/global_payout",
                "type": "collections",
                "publicKey": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAt/RD+L0L5T1rK212Yv89\nhvbES7DEwgMNvj22xlEij/7Orl6CgEQDuXisjHFqiIWe05tpR6AMWlRrggb9O+kw\nZsMrHWOp9SNcNIsR8rka5fqVSbYE8mXqtw4f4MUbB8AnRQRYIyXvlxMT1eWlXTJo\nokHsiYanA2zx3uXkDs/Ia+8B2/xKvK3UUbVa2I/b+MIWk7y02wHGFE9Zu4J98+uA\nJluS9GUEyGRtxyb+muoApGlxV9j0Qw8zhr1VPb5sjOzGKwAYfiNGNZoE59BFYM9E\nM7PfO+JWSGc6RHwNSsLxVKoj42zv6LQ2nhJ15YMuVKVD5Hb57oR6hQantzZaA3gE\n5wIDAQAB\n-----END PUBLIC KEY-----\n",
                "status": "active"
            }
    }

Delete Webhook
~~~~~~~~~~~~~~
Ready to clean up? Deleting a webhook is simple:

.. code-block:: console

    DELETE https://sandbox.hurupay.com/v1/webhook/{webhookId}

**Request Response**

You’ll receive a confirmation like this:

.. code-block:: javascript

    {
        "success": true,
        "message": "Webhook deleted successfully",
        "data": {}
    }

Webhook Signature Verification
-------------------------------

Each webhook sent will include a signature in the header with `x-webhook-signature`, which consists of the request body. This can be verified using the webhook's public key.

**Javascript Verification Function**

.. code-block:: javascript

    import crypto from 'crypto';

    function verifyWebhookSignature(body: string, signature: string, publicKey: string): boolean {
        const hash = crypto.createHash('SHA256');
        hash.update(body);
        const hashedData = hash.digest('hex');

        // Create a verifier for SHA256
        const verifier = crypto.createVerify('SHA256');
        verifier.update(hashedData);
        verifier.end();

        // Verify the signature using the public key
        return verifier.verify(publicKey, Buffer.from(signature, 'base64'));
    }

**Ruby Verification Function**

.. code-block:: ruby

    require 'openssl'
    
    def verify_webhook_signature(body, signature, public_key)
      hashed_data = OpenSSL::Digest::SHA256.hexdigest(body)
      verifier = OpenSSL::PKey::RSA.new(public_key)
      verifier.verify(OpenSSL::Digest::SHA256.new, Base64.decode64(signature), hashed_data)
    end

**Python Verification Function**

.. code-block:: python

    import hashlib
    import base64
    from Crypto.PublicKey import RSA
    from Crypto.Signature import pkcs1_15
    
    def verify_webhook_signature(body: str, signature: str, public_key: str) -> bool:
        hashed_data = hashlib.sha256(body.encode()).digest()
        rsa_key = RSA.import_key(public_key)
        
        try:
            pkcs1_15.new(rsa_key).verify(hashed_data, base64.b64decode(signature))
            return True
        except (ValueError, TypeError):
            return False

**Go Verification Function**

.. code-block:: go

    package main
    
    import (
        "crypto/rsa"
        "crypto/sha256"
        "encoding/base64"
        "errors"
    )
    
    func verifyWebhookSignature(body string, signature string, publicKey *rsa.PublicKey) (bool, error) {
        hashedData := sha256.Sum256([]byte(body))
        decodedSignature, err := base64.StdEncoding.DecodeString(signature)
        if err != nil {
            return false, err
        }

        err = rsa.VerifyPKCS1v15(publicKey, crypto.SHA256, hashedData[:], decodedSignature)
        if err != nil {
            return false, errors.New("signature verification failed")
        }
        return true, nil
    }


Webhook/Event Structure
-------------------------------

We have launched webhooks for Collections, Payouts, and User KYC, and we plan to expand support to additional event categories in the coming weeks.

Your feedback is essential to us. Please feel free to suggest any priority event categories you would like us to focus on for future updates.

Below is a successful event for collections

.. code-block:: javascript

        {
            api_version: 'v1',
            event_id: '1234567890abcdef',
            event_category: 'collection',
            event_type: 'collection.successful',
            event_object: {
                type: 'collections',
                id: 'col_9876543210abcdef',
                partner: 'partner_ABC123',
                customer_name: 'John Doe',
                collection_currency: 'GHS',
                collection_rail: 'MTN',
                collection_amount: 5000,
                blockchain_network: 'CELO',
                blockchain_token: 'cUSD',
                blockchain_proof: 'https://explorer.celo.org/alfajores/tx/0xabc123def456gh7890ijklmnopqrs123456',
                token_amount: 500,
                description: 'Mobile collection for invoice #INV-2024-001',
            },
            event_created_at: '2024-10-10',
        };


Event Definition
-------------------------------

As illustrated in the event samples above, each webhook event includes the following fields:

-  `api_version` : Currently set to `v1`, which is the version in use by Hurupay APIs.

-  `event_id` : A globally unique identifier assigned to this event.

-  `event_category` :

  - `collections`
  - `payouts`
  - `kyc`

- `event_type` : Structured as "<event_category>.<mutation_type>".


Possible mutation types include:

- `created`
- `updated`
- `canceled`
- `failed`
- `successful`
- `declined`

Examples of event types:
-------------------------------

Collections:
-------------------------------

- `collections.created`
- `collections.declined`
- `collections.failed`
- `collections.successful`

Payouts:
-------------------------------

- `payouts.declined`
- `payouts.successful`

KYC:
-------------------------------

- `kyc.created`
- `kyc.updated`
- `kyc.failed`
- `kyc.successful`
