---
title: Azure Scvmm client library for JavaScript
keywords: Azure, javascript, SDK, API, @azure/arm-scvmm, scvmm
ms.date: 02/03/2023
ms.topic: reference
ms.devlang: javascript
ms.service: scvmm
---
# Azure Scvmm client library for JavaScript - version 1.0.0-beta.3 


This package contains an isomorphic SDK (runs both in Node.js and in browsers) for Azure Scvmm client.

The Microsoft.ScVmm Rest API spec.

[Source code](https://github.com/Azure/azure-sdk-for-js/tree/@azure/arm-scvmm_1.0.0-beta.3/sdk/scvmm/arm-scvmm) |
[Package (NPM)](https://www.npmjs.com/package/@azure/arm-scvmm) |
[API reference documentation](/javascript/api/@azure/arm-scvmm?view=azure-node-preview) |
[Samples](https://github.com/Azure-Samples/azure-samples-js-management)

## Getting started

### Currently supported environments

- [LTS versions of Node.js](https://github.com/nodejs/release#release-schedule)
- Latest versions of Safari, Chrome, Edge and Firefox.

See our [support policy](https://github.com/Azure/azure-sdk-for-js/blob/@azure/arm-scvmm_1.0.0-beta.3/SUPPORT.md) for more details.

### Prerequisites

- An [Azure subscription][azure_sub].

### Install the `@azure/arm-scvmm` package

Install the Azure Scvmm client library for JavaScript with `npm`:

```bash
npm install @azure/arm-scvmm
```

### Create and authenticate a `Scvmm`

To create a client object to access the Azure Scvmm API, you will need the `endpoint` of your Azure Scvmm resource and a `credential`. The Azure Scvmm client can use Azure Active Directory credentials to authenticate.
You can find the endpoint for your Azure Scvmm resource in the [Azure Portal][azure_portal].

You can authenticate with Azure Active Directory using a credential from the [@azure/identity][azure_identity] library or [an existing AAD Token](https://github.com/Azure/azure-sdk-for-js/blob/@azure/arm-scvmm_1.0.0-beta.3/sdk/identity/identity/samples/AzureIdentityExamples.md#authenticating-with-a-pre-fetched-access-token).

To use the [DefaultAzureCredential][defaultazurecredential] provider shown below, or other credential providers provided with the Azure SDK, please install the `@azure/identity` package:

```bash
npm install @azure/identity
```

You will also need to **register a new AAD application and grant access to Azure Scvmm** by assigning the suitable role to your service principal (note: roles such as `"Owner"` will not grant the necessary permissions).
Set the values of the client ID, tenant ID, and client secret of the AAD application as environment variables: `AZURE_CLIENT_ID`, `AZURE_TENANT_ID`, `AZURE_CLIENT_SECRET`.

For more information about how to create an Azure AD Application check out [this guide](/azure/active-directory/develop/howto-create-service-principal-portal).

```javascript
const { Scvmm } = require("@azure/arm-scvmm");
const { DefaultAzureCredential } = require("@azure/identity");
// For client-side applications running in the browser, use InteractiveBrowserCredential instead of DefaultAzureCredential. See https://aka.ms/azsdk/js/identity/examples for more details.

const subscriptionId = "00000000-0000-0000-0000-000000000000";
const client = new Scvmm(new DefaultAzureCredential(), subscriptionId);

// For client-side applications running in the browser, use this code instead:
// const credential = new InteractiveBrowserCredential({
//   tenantId: "<YOUR_TENANT_ID>",
//   clientId: "<YOUR_CLIENT_ID>"
// });
// const client = new Scvmm(credential, subscriptionId);
```


### JavaScript Bundle
To use this client library in the browser, first you need to use a bundler. For details on how to do this, please refer to our [bundling documentation](https://aka.ms/AzureSDKBundling).

## Key concepts

### Scvmm

`Scvmm` is the primary interface for developers using the Azure Scvmm client library. Explore the methods on this client object to understand the different features of the Azure Scvmm service that you can access.

## Troubleshooting

### Logging

Enabling logging may help uncover useful information about failures. In order to see a log of HTTP requests and responses, set the `AZURE_LOG_LEVEL` environment variable to `info`. Alternatively, logging can be enabled at runtime by calling `setLogLevel` in the `@azure/logger`:

```javascript
const { setLogLevel } = require("@azure/logger");
setLogLevel("info");
```

For more detailed instructions on how to enable logs, you can look at the [@azure/logger package docs](https://github.com/Azure/azure-sdk-for-js/tree/@azure/arm-scvmm_1.0.0-beta.3/sdk/core/logger).

## Next steps

Please take a look at the [samples](https://github.com/Azure-Samples/azure-samples-js-management) directory for detailed examples on how to use this library.

## Contributing

If you'd like to contribute to this library, please read the [contributing guide](https://github.com/Azure/azure-sdk-for-js/blob/@azure/arm-scvmm_1.0.0-beta.3/CONTRIBUTING.md) to learn more about how to build and test the code.

## Related projects

- [Microsoft Azure SDK for JavaScript](https://github.com/Azure/azure-sdk-for-js)



[azure_cli]: /cli/azure
[azure_sub]: https://azure.microsoft.com/free/
[azure_sub]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[azure_identity]: https://github.com/Azure/azure-sdk-for-js/tree/@azure/arm-scvmm_1.0.0-beta.3/sdk/identity/identity
[defaultazurecredential]: https://github.com/Azure/azure-sdk-for-js/tree/@azure/arm-scvmm_1.0.0-beta.3/sdk/identity/identity#defaultazurecredential

