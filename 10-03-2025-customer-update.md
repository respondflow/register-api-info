# Volt Register API planned changes

## Breaking Changes

The following items are either planned, in development, or unreleased. We will update our [API reference](https://register-sandbox.ascri.be/docs) and also provide a changelog for easier integration with future changes.

We are working on our versioning system to ensure that future changes don't break the implementation on your end. Please bear with us.

## New routing structure

We are working to make our API more RESTful. Some routes may change. No functionality will change, but the endpoint might. All changes will be documented in our API reference and provide a changelog for easier integration.

## Better error responses

The HTTP error codes returned from the API will not change, but the response format will in order to provide more details. Eventually, all of our API's will follow a common error response format.

Here are a few of the things we are considering, we welcome your feedback.

**Validation:**
```json
{
  "errors": [
    {
      "kind": "validation",
      "status": 422,
      "details": [
        {
          "key": "city",
          "message": "is required",
          "uiFacing": true,
          "errorCode": "VE02001"
        },
        {
          "key": "contact_email",
          "message": "is greater than 100 characters",
          "uiFacing": true,
          "errorCode": "VE02003"
        }
      ]
    }
  ]
}
```

**Schema:**
```json
{
  "errors": [
    {
      "kind": "schema",
      "status": 422,
      "details": [
        {
          "message": "Invalid relationship found",
          "uiFacing": false,
          "errorCode": "VE03002"
        }
      ]
    }
  ]
}
```

**General:**
```json
{
  "errors": [
    {
      "kind": "general",
      "status": 500,
      "details": [
        {
          "message": "An unknown error occurred",
          "retryable": false,
          "uiFacing": false,
          "errorCode": "VE01001"
        }
      ]
    }
  ]
}
```

## HTTP responses with meta data updated

Requests to endpoints fetching multiple resources will respond with a `meta` section. This section now includes a `total_count` field under `pagination`. See below. Please note that additional fields may be added in the future.

Example:

```json
{
  "data": {}, // data here
  "meta": {
    "pagination": {
      "page": 1, // the current page
      "per_page": 10, // records per page
      "total_count": 100 // the total number of records
    }
  }
}
```

## Better sorting of resources

API endpoints that return multiple resources will have the ability to be sorted by fields in both the top level `data` field and the `item` field.

## Webhooks

Webhooks will allow API consumers to track changes in status or other fields made to registrations as it makes its way to approval.

This system is in the planning phase. If you have thoughts on the kind of data you would like to see included, please get in contact with us. As we elaborate this system in the coming weeks we will update you with those details.
