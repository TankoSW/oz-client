# @tanko/oz-client

> **Generated file:** this package is generated using [openapi-typescript](https://openapi-ts.dev/introduction), [openapi-fetch](https://openapi-ts.dev/openapi-fetch/) and by doing code generation from the OpenAPI schema of a private project called Oz.

This package provides a typed client for the Oz API generated from an OpenAPI schema.

## Usage

The client exposes functions to create new clients, allows you the same degree of customization `openapi-fetch` allows since its a wrapper of it. It also exposes facade functions that let you discover what the API can do without looking at docs from the endpoint paths.

```ts
import { createOzClient } from "@tanko/oz-client";

const client = createOzClient({
  baseUrl: "https://example.com",
});

const response = await client.patients.list();

if (response.error) {
  throw response.error;
}

console.log(response.data);
```

The underlying openapi-fetch client is also available as client.raw_client for direct path-based calls:

```ts
const response = await client.raw_client.GET("/api/v1/patient");
```

As said before, the create functions accepts the regular `openapi-fetch` client options, together
with default onRequest, onResponse, and onError callbacks which can be overridden for custom behaviour:

```ts
const client = createOzClient({
  baseUrl: "https://example.com",
  onRequest: ({ request }) => {
    request.headers.set("Authorization", `Bearer ${token}`);
  },
  onResponse: ({ response }) => {
    console.log(response.status);
  },
});

await client.patients.list({
  onRequest: ({ request }) => {
    request.headers.set("X-Request-Mode", "debug");
  },
});
```

The generated paths, operations, and components types are re-exported. Component schemas are also available as direct aliases:

```ts
import type { Patient, components } from "@tanko/oz-client";

const patient: Patient = /* ... */;
type User = components["schemas"]["User"];
```

