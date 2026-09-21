# @tanko/oz-client

> **Generated file:** this package is produced by cargo xtask build-client.
> Do not edit this directory directly; changes will be overwritten the next
> time the client is generated.

This package provides a typed client for the Oz API. The generated
codegen.d.ts file is the source of truth for endpoint and schema types.

## Usage

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

Grouped methods preserve the request and response types generated from the
OpenAPI schema. The underlying openapi-fetch client is also available as
client.raw_client for direct path-based calls:

```ts
const response = await client.raw_client.GET("/api/v1/patient");
```

## Request lifecycle callbacks

createOzClient accepts the regular openapi-fetch client options, together
with default onRequest, onResponse, and onError callbacks:

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
```

Callbacks can be overridden for an individual grouped method call:

```ts
await client.patients.list({
  onRequest: ({ request }) => {
    request.headers.set("X-Request-Mode", "debug");
  },
});
```

## Generated types

The generated paths, operations, and components types are re-exported.
Component schemas are also available as direct aliases:

```ts
import type { Patient, components } from "@tanko/oz-client";

const patient: Patient = /* ... */;
type User = components["schemas"]["User"];
```

