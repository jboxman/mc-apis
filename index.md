---
layout: default
title: Mastercard Documentation API reference
---

# Mastercard Documentation API reference

## Overview

The Mastercard Documentation API is HTTP-based and available through a set of HTTPS URLs. All traffic is encrypted with a TLS certificate.

The API endpoint is `https://mastercarddocuments.apis.com`.

This API reference documentation covers the following topics:

- Getting started
- Security considerations
- Rate limiting and retries
- HTTP requests and responses
  * HTTP body encoding
  * HTTP response encoding
  * HTTP response data
- API endpoints
  * Creating a new document
  * Retrieving an existing document
  * Deleting an existing document
- Common status codes

## Getting started

To use the Mastercard Documentation APIs you'll need an API key. You can get an API key from the Mastercard Documentation portal after you have created a new project.

## Security considerations

This section describes the minimum requirements and recommendations for TLS versions, ciphers, and API key handling.

## Rate limiting and retries

This section describes how frequently you can make API requests and how to gracefully handle retries in the event of a temporary failure.

## HTTP requests and responses

The following sections describe the HTTP body and response encodings and the response payload for the APIs.

## HTTP body encoding

For APIs that require a body payload, such as when creating a new document, you must specify  `Content-Type: application/json`. For example:

```
POST /documents
Content-type: application/json
{"documentId ": "aaaab987", "documentTitle": "A document"}
```

## HTTP response encoding

For APIs that provide a response payload, such as when retrieving an existing document, the return type is `Content-Type: application/json`.

## HTTP response data

If you create a new document or retrieve an existing document, the response is a JSON document that includes the following fields:

- `document`: An object describing the created document
- `document.CreatedTimestamp`: The creation time for the document
- `document.documentId`: The identifier of the document
- `document.documentTitle`: The title of the document

The following is an example response body:

```json
{
  "document": {
    "CreatedTimestamp": "tz",
    "documentId": "string",
    "documentTitle": "string"
  }
}
```

## API endpoints

The following sections describe the available Mastercard Documentation APIs.

### Creating a new document

- Method: `POST /documents`
- Parameters:
  * `apikey={consumerkey}`: Specify your API authentication key
- Payload type: `application/json`
- Response body type: `application/json`
- Response codes:
  * `200` – OK
  * For other codes see _Common status codes_

In the following example a new document is created:

```
$ echo "{"documentId ": "aaaab987", "documentTitle": "A document"}" > doc.json
$ curl -X POST -H "Content-Type: application/json" -d@doc.json \
    https://mastercarddocuments.apis.com/documents?apikey=7890
```

### Retrieving an existing document

- Method: `GET /documents/{documentId}`
- Parameters:
  * `apikey={consumerkey}`: Specify your API authentication key
- Payload type: None
- Response body type: `application/json`
- Response codes:
  * `200` – OK
  * For other codes see _Common status codes_

In the following example an existing document is retrieved:

```
$ curl https://mastercarddocuments.apis.com/documents/aaaab987?apikey=7890
```


### Deleting an existing document

- Method: `DELETE /documents/{documentId}`
- Parameters:
  * `apikey={consumerkey}`: Specify your API authentication key
- Response codes:
  * `204` – No Content
  * For other codes see _Common status codes_

In the following example an existing document is deleted:

```
$ curl -X DELETE  \
    https://mastercarddocuments.apis.com/documents/aaaaab987?apikey=7890
```

## Common status codes

The following HTTP status codes are common to all of the API endpoints.

* `200` – OK
* `204` - No Content
* `400` - Bad Request
* `401` - Unauthorized
* `402` - Request Failed
* `403` - Forbidden
* `404` - Not Found
* `500`, `502`, `503`, `504` - Server Error
