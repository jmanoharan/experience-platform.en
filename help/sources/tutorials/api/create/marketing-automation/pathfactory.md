---
title: Create a PathFactory Base Connection Using the Flow Service API
description: Learn how to authenticate your PathFactory account against Experience Platform using the Flow Service API.
exl-id: 
---
# Create a [!DNL PathFactory] base connection using the [!DNL Flow Service] API

A base connection represents the authenticated connection between a source and Adobe Experience Platform.

This tutorial walks you through the steps to create a base connection for [!DNL PathFactory] using the [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Getting started

This guide requires a working understanding of the following components of Adobe Experience Platform:

* [Sources](../../../../home.md): Experience Platform allows data to be ingested from various sources while providing you with the ability to structure, label, and enhance incoming data using Platform services.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform provides virtual sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Using Platform APIs

For information on how to successfully make calls to Platform APIs, see the guide on [getting started with Platform APIs](../../../../../landing/api-guide.md).

The following section provides additional information that you will need to know in order to successfully connect to [!DNL PathFactory] using the [!DNL Flow Service] API.

### Gather Required Credentials {#gather-credentials}

To access your PathFactory account on the Platform, you must provide the following values:

| Credential | Description |
| ---------- | ----------- |
| Username | Your PathFactory account username. This is essential for identifying your account in the system. |
| Password | The password associated with your PathFactory account. Ensure this is kept secure to prevent unauthorized access. |
| Domain | The domain associated with your PathFactory account. This typically refers to the unique identifier within your PathFactory URL. |
| Access Token | A unique token used for API authentication to ensure secure communication between your systems and PathFactory. |
| API Endpoints | Specific API endpoints for accessing data: Visitors, Sessions, and Page Views. Each endpoint corresponds to different data sets you can retrieve. **Note:** These are pre-defined by PathFactory and are specific to the data you intend to access:
  - **Visitors Endpoint**: `/api/public/v3/data_lake_apis/visitors.json`
  - **Sessions Endpoint**: `/api/public/v3/data_lake_apis/sessions.json`
  - **Page Views Endpoint**: `/api/public/v3/data_lake_apis/page_views.json`

For detailed guidance on how to secure and use your credentials, and for information about obtaining and refreshing your access token, visit the [PathFactory Support Center](https://support.pathfactory.com/categories/adobe/). This resource offers comprehensive guides on managing your credentials and ensuring effective and secure API integration.

## Create a base connection

A base connection retains information between your source and Platform, including your source's authentication credentials, the current state of the connection, and your unique base connection ID. The base connection ID allows you to explore and navigate files from within your source and identify the specific items that you want to ingest, including information regarding their data types and formats.

To create a base connection ID, make a POST request to the `/connections` endpoint while providing your [!DNL PathFactory] authentication credentials as part of the request body.

**API format**

```https
POST /connections
```

**Request**

The following request creates a base connection for [!DNL PathFactory]:

```shell
curl --location 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {{authorizationToken}}' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{API_KEY}}' \
--header 'x-gw-ims-org-id: {{ORG_ID}}' \
--header 'x-sandbox-name: {{SANDBOX_NAME}}' \
--data '{
      "name": "Basic Authentication",
      "description": "Basic Authentication",
      "connectionSpec": {
          "id": "20d50f2a-1ffa-40f8-a43d-87c1516dbdc5",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "domain": "{subDomainID}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Property               | Description |
|------------------------| --- |
| `name`                 | The name of your base connection. Ensure that the name of your base connection is descriptive as you can use this to look up information on your base connection. |
| `description`          | (Optional) A property that you can include to provide more information on your base connection. |
| `connectionSpec.id`    | The connection specification ID of your source. This ID can be retrieved after your source is registered and approved through the [!DNL Flow Service] API. |
| `auth.specName`        | The authentication type that you are using to connect your source to Platform. |
| `auth.params.domain`     | (Optional) The subDomain name/id for your organization is used to validate credentials when creating a base connection. If unprovided, credentials are automatically checked during the source connection creation step instead. |
| `auth.params.username` | The username that corresponds with your [!DNL Pathfactory] account. This is required for basic authentication. |
| `auth.params.password` | The password that corresponds with your [!DNL Pathfactory] account. This is required for basic authentication. |

**Response**

A successful response returns the newly created connection, including its unique connection identifier (`id`). This ID is required to explore your data in the next tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Next steps

By following this tutorial, you have created a [!DNL PathFactory] base connection using the [!DNL Flow Service] API. You can use this base connection ID in the following tutorials:

* [Explore the structure and contents of your data tables using the [!DNL Flow Service] API](../../explore/tabular.md)
* [Create a dataflow to bring marketing automation data to Platform using the [!DNL Flow Service] API](../../collect/marketing-automation.md)
