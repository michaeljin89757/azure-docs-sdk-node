---
title: Azure Communication Identity client library for JavaScript
keywords: Azure, javascript, SDK, API, @azure/communication-identity, communication
ms.date: 03/26/2024
ms.topic: reference
ms.devlang: javascript
ms.service: communication
---
# Azure Communication Identity client library for JavaScript - version 1.3.1 


The identity library is used for managing users and tokens for Azure Communication Services.

## Getting started

### Prerequisites

- An [Azure subscription][azure_sub].
- An existing Communication Services resource. If you need to create the resource, you can use the [Azure Portal][azure_portal], the [Azure PowerShell][azure_powershell], or the [Azure CLI][azure_cli].

### Installing

```bash
npm install @azure/communication-identity
```

### Browser support

#### JavaScript Bundle

To use this client library in the browser, first you need to use a bundler. For details on how to do this, please refer to our [bundling documentation](https://aka.ms/AzureSDKBundling).

## Key concepts

### Clients

The `CommunicationIdentityClient` provides methods to manage users and their tokens.

## Examples

## Authentication

You can get a key and/or connection string from your Communication Services resource in [Azure Portal][azure_portal]. Once you have a key, you can authenticate the `CommunicationIdentityClient` with any of the following methods:

### Create `KeyCredential` with `AzureKeyCredential` before initializing the client

```typescript
import { AzureKeyCredential } from "@azure/core-auth";
import { CommunicationIdentityClient } from "@azure/communication-identity";

const credential = new AzureKeyCredential(KEY);
const client = new CommunicationIdentityClient(ENDPOINT, credential);
```

### Using a connection string

```typescript
import { CommunicationIdentityClient } from "@azure/communication-identity";

const connectionString = `endpoint=ENDPOINT;accessKey=KEY`;
const client = new CommunicationIdentityClient(connectionString);
```

### Using a `TokenCredential`

```typescript
import { DefaultAzureCredential } from "@azure/identity";
import { CommunicationIdentityClient } from "@azure/communication-identity";

const credential = new DefaultAzureCredential();
const client = new CommunicationIdentityClient(ENDPOINT, credential);
```

If you use a key to initialize the client you will also need to provide the appropriate endpoint. You can get this endpoint from your Communication Services resource in [Azure Portal][azure_portal].

## Usage

### Creating an instance of CommunicationIdentityClient

```typescript
import { CommunicationIdentityClient } from "@azure/communication-identity";

const client = new CommunicationIdentityClient(CONNECTION_STRING);
```

### Creating a new user

Use the `createUser` method to create a new user.

```typescript
const user = await client.createUser();
```

### Creating and refreshing a user token

Use the `getToken` method to issue or refresh a token for an existing user. The method also takes in a list of communication token scopes. Scope options include:

- `chat` (Use this for full access to Chat APIs)
- `voip` (Use this for full access to Calling APIs)
- `chat.join` (Access to Chat APIs but without the authorization to create, delete or update chat threads)
- `chat.join.limited` (A more limited version of chat.join that doesn't allow to add or remove participants)
- `voip.join` (Access to Calling APIs but without the authorization to start new calls)

```typescript
let { token } = await client.getToken(user, ["chat"]);
```

To refresh the user token, issue another token with the same user.

```typescript
let { token } = await client.getToken(user, ["chat"]);
```

### Creating a user token with custom expiration

It's also possible to create a Communication Identity access token by customizing the expiration time. Validity period of the token must be within [60,1440] minutes range. If not provided, the default value of 1440 minutes (24 hours) will be used.

```typescript
const tokenOptions: GetTokenOptions = { tokenExpiresInMinutes: 60 };
let { token } = await client.getToken(user, ["chat"], tokenOptions);
```

### Creating a user and a token in a single request

For convenience, use `createUserAndToken` to create a new user and issue a token with one function call. This translates into a single web request as opposed to creating a user first and then issuing a token.

```typescript
let { user, token } = await client.createUserAndToken(["chat"]);
```

### Creating a user and a token with custom expiration in a single request

It's also possible to create a Communication Identity access token by customizing the expiration time. Validity period of the token must be within [60,1440] minutes range. If not provided, the default value of 1440 minutes (24 hours) will be used.

```typescript
const userAndTokenOptions: CreateUserAndTokenOptions = { tokenExpiresInMinutes: 60 };
let { user, token } = await client.createUserAndToken(["chat"], userAndTokenOptions);
```

### Revoking tokens for a user

Use the `revokeTokens` method to revoke all issued tokens for a user.

```typescript
await client.revokeTokens(user);
```

### Deleting a user

Use the `deleteUser` method to delete a user.

```typescript
await client.deleteUser(user);
```

### Exchanging Azure AD access token of a Teams User for a Communication access token

Use `getTokenForTeamsUser` method to exchange an Azure AD access token of a Teams user for a new `CommunicationAccessToken` with a matching expiration time.

```typescript
await client.getTokenForTeamsUser({
  teamsUserAadToken: "<aad-access-token-of-a-teams-user>",
  clientId: "<cliend-id-of-an-aad-application>",
  userObjectId: "<aad-object-id-of-a-teams-user>",
});
```

## Troubleshooting

## Next steps

Please take a look at the
[samples](https://github.com/Azure/azure-sdk-for-js/blob/@azure/communication-identity_1.3.1/sdk/communication/communication-identity/samples)
directory for detailed examples on how to use this library.

## Contributing

If you'd like to contribute to this library, please read the [contributing guide](https://github.com/Azure/azure-sdk-for-js/blob/@azure/communication-identity_1.3.1/CONTRIBUTING.md) to learn more about how to build and test the code.

## Related projects

- [Microsoft Azure SDK for Javascript](https://github.com/Azure/azure-sdk-for-js)

[azure_cli]: /cli/azure
[azure_sub]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[azure_powershell]: /powershell/module/az.communication/new-azcommunicationservice



