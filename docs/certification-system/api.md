---
layout: default
title: API
parent: Certification System
nav_order: 3
---

# Certification **API**
{: .no_toc }

Let's talk about the available API endpoints, even though they are all documented in the API itself! 🤠 
{: .fs-6 .fw-300 }

## Available endpoints
{: .no_toc .text-delta }

1. TOC
{:toc}

<!-- todo: link a Swagger. -->

## Refresh the rulesets

This **POST** operation overrides the default ruleset with a custom one with the same structure.

<div class="code-example" markdown="1">
E.g.:

```bash
curl --location --request POST 'http://localhost:8080/apifirst/v1/rulesets/refresh'
```
</div>

<br>

## Verify a file

This **POST** operation verifies the retrieved file's content as long as it complies with the OpenAPI specification. 

<div class="code-example" markdown="1">
E.g.:

```bash
curl --location --request POST 'http://localhost:8080/apifirst/v1/file-verify-protocol' \--header 'Content-Type: multipart/form-data' \--header 'Accept: application/json' \--form 'url="https://raw.githubusercontent.com/..."' \--form 'apiProtocol="1"'
```
</div>

<br>

## Validate a ZIP file

This **POST** operation creates a validation result from a ZIP file (which should contain a repository) or from a repository URL. 

<div class="code-example" markdown="1">
E.g.:

```bash
curl --location --request POST 'http://localhost:8080/apifirst/v1/validations' \--header 'Content-Type: multipart/form-data' \--header 'Accept: application/json' \--form 'url="https://github.com/..."' \--form 'validationType="1"' \--form 'isVerbose="false"'
```
</div>

Take into account that you need the following **repository structure** to use the `validations` request with a ZIP:

```
├── metadata.yml
└── myApis
    └── samples
        ├── asyncapi-streams
        │   ├── asyncapi.yml
        │   ├── cart_lines_operations.avsc
        │   └── lines_operations_event.avsc
        └── rest
            └── openapi-rest.yml
```

Being the `metadata.yml` a file that contains all APIs defined in the repo:

```yml
apis:
 - name: # The API name
   api-spec-type:   # API type: grpc, event, rest
   definition-path: # Path to API folder
   definition-file: # API definition file
```

<div class="code-example" markdown="1">
For example:

```yml
apis:
  - name: "REST Sample"
    api-spec-type: rest
    definition-path: myApis/samples/rest
    definition-file: openapi-rest.yml
  - name: "AsyncAPI Streams Sample"
    api-spec-type: event
    definition-path: myApis/samples/asyncapi-streams
    definition-file: asyncapi.yml
```
</div>