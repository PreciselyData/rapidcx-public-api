---
stoplight-id: nn3y754p5uo7g
---

# About API Versioning

The RapidCX API is continuously evolving with new features, improvements, and bug fixes. As a result, changes are expected and will be documented accordingly. 
However, some changes or additions are backward-compatible and your applications should be flexible enough to handle them. These changes will not impact the RapidCX API version.

## Backward compatible changes
Backward compatible are changes to the API that do not affect existing consumer implementations. These include:
- Adding a new field in an outbound payload
- Marking a required request parameter as optional
- Adding an optional request parameter to existing API methods
- Changing the order of properties in existing API responses (JSON by definition is an object of unordered key/value pairs).
- Adding a new endpoint
- Redefining error codes in order to provide more context (e.g. changing a response from 500 (INTERNAL SERVER ERROR) to 401 (UNAUTHORIZED))
- Extending the scope of a request parameter (e.g., starting to accept more possible values)

## Backward incompatible changes
Backward incompatible changes are changes to the API that may affect existing consumer implementations and may require reimplementing the behavior of the API. These include:
- Removing a mandatory field of an outbound payload (e.g. removing an existing property important_property in one of the payloads that we are sending).
- Renaming a field (this may require keeping the deprecated old naming for a reasonable amount of time, before removing it completely).
- Adding a required request parameter on one of the existing endpoints;
- Removing a non-optional field from the request's response
- Removing the entire API endpoint
- Removing enum values
- Making a previously optional parameter required

# Specifying an API version

The RapidCX API uses request header versioning. Where it is required you need to use the `RapidCX-Api-Version` header parameter to specify an API version. Each request, where it is indicated in the API specification, should contain a version header in the following format:

**Example:** `RapidCX-Api-Version: 2025-02-13`

The `RapidCX-Api-Version` header is **optional**, the endpoint will default to the newest released API version if the header is not provided.

The RapidCX API will return a 400 error response in the following cases when versioning is required:
- Using an invalid `RapidCX-Api-Version` header, invalid values include:
  - non-existent API versions,
  - API versions removed from the list of supported versions


## Deprecated endpoints

Endpoints marked as deprecated will remain functional **until the Sunset date** and will not be decommissioned, ensuring the uninterrupted operation of existing integrations.

Nevertheless, it is strongly advised to transition to newer versions to benefit from the latest features, enhancements, and support. Updating integrations to the latest versions ensures continued compatibility and optimal performance as the API evolves.

## Upgrading to a new API version

Before upgrading to a new REST API version, you should read the changelog of breaking changes for the new API version to understand what breaking changes are included and to learn more about how to upgrade to that specific API version. For more information, see Breaking changes.

When you update your integration to specify the new API version in the `RapidCX-Api-Version` header, you'll also need to make any changes required for your integration to work with the new API version.

Once your integration is updated, test your integration to verify that it works with the new API version.


