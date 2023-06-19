---
layout: default
title: API
parent: Scoring System
nav_order: 3
---

# Scoring **API**
{: .no_toc }

Let's talk about the available API endpoints, even though they are all documented in the API itself! 🤠 
{: .fs-6 .fw-300 }


## Available endpoints
{: .no_toc .text-delta }

1. TOC
{:toc}

## Verify a file

This **POST** operation verifies the retrieved file's content as long as it complies with the OpenAPI specification.

You can verify a file in two ways:

- You can indicate the specification file and type in a JSON with the URL and `apiProtocol` property.
  <div class="code-example" markdown="1">
  E.g.:

  ```bash
  curl --location 'http://localhost:8080/apifirst/v1/apis/verify' \ 
  --header 'Content-Type: application/json' \ 
  --data '{ 
    "url": "https://raw.githubusercontent.com/InditexTech/api-scoring-engine/main/packages/api-cli/samples/myApis/rest/contract/openapi-rest.yml", 
    "apiProtocol": "REST" 
  }' 
  ```
  </div>

- You can attach the specification file along with the API specification type in the `apiProtocol` property.

  <div class="code-example" markdown="1">
  E.g.:

  ```bash
  curl --location 'http://localhost:8080/apifirst/v1/apis/verify' \
  --header 'Content-Type: multipart/form-data' \
  --form 'file=@"/myApis/rest/contract/openapi-rest.yml"' \
  --form 'apiProtocol="REST"'
  ```
  </div>

<table>
  <thead>
    <tr>
      <th style="color:#6852D0;">Input type</th>
      <th style="color:#6852D0;">Parameters</th>
      <th style="color:#6852D0;">Description</th>
      <th style="color:#6852D0;">Required</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan= "2">Application/JSON</td>
      <td>url</td>
      <td>URL to the API Specification file in the repository. For example: https://raw.githubusercontent.com/InditexTech/api-scoring-engine/main/packages/api-cli/samples/myApis/rest/contract/openapi-rest.yml</td>
      <td>yes</td>
    </tr>
    <tr>
      <td>apiProtocol</td>
      <td>Protocol type that you want to validate. Possible values: "REST", "EVENT" or "GRPC".</td>
      <td>yes</td>
    </tr>
    <tr>
      <td rowspan= "2">Multipart/form-data</td>
      <td>File</td>
      <td>Binary API specification file.</td>
      <td>yes</td>
    </tr>
    <tr>
      <td>apiProtocol</td>
      <td>Protocol type that you want to validate. Possible values: "REST", "EVENT" or "GRPC".</td>
      <td>yes</td>
    </tr>
  </tbody>
</table>

<br>

## Validate a ZIP file

You can certify an API by retrieving a ZIP file of a compressed folder. The folder needs the following **repository structure** to use the `validations` request with a ZIP:

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

This **POST** operation creates a validation result from a ZIP file (which should contain a repository) or from a repository URL.

You can verify a ZIP file in two ways:

- In the JSON input type, you can retrieve the ZIP file with the required structure setting the `URL` to it and indicating the parameters you want to validate (Design, Security, Documentation, or all of them) in the `validationType` property.

  <div class="code-example" markdown="1">
  E.g.:

  ```bash
  curl --location 'http://localhost:8080/apifirst/v1/apis/validate' \ 
  --header 'Content-Type: multipart/form-data' \ 
  --header 'Accept: application/json' \ 
  --form 'file=@"/samples/apisGrade.zip"' \ 
  --form 'validationType="DESIGN"' 
  ```
  </div>

- In the form-data input type, you can retrieve the ZIP file with the required structure along with the parameters you want to validate (Design, Security, Documentation, or all of them) in the `validationType` property.

  <div class="code-example" markdown="1">
  E.g.:

  ```bash
  curl --location 'http://localhost:8080/apifirst/v1/apis/validate' \ 
  --header 'Content-Type: application/json' \ 
  --data '{ 
    "url": "https://github.com/raw/main/myApis.zip", 
    "isVerbose": false, 
    "validationType": "DESIGN"
  }'
  ```
  </div>

<table>
  <thead>
    <tr>
      <th style="color:#6852D0;">Input type</th>
      <th style="color:#6852D0;">Parameters</th>
      <th style="color:#6852D0;">Description</th>
      <th style="color:#6852D0;">Required</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan= "3">Application/JSON</td>
      <td>url</td>
      <td>URL to the API Specification file in the repository. For example: https://raw.githubusercontent.com/InditexTech/api-scoring-engine/main/packages/api-cli/samples/main.zip</td>
      <td>yes</td>
    </tr>
    <tr>
      <td>isVerbose</td>
      <td>Boolean attribute that activates the debug mode.</td>
      <td>no</td>
    </tr>
    <tr>
      <td>validationType</td>
      <td>Scoring module that the microservice evaluates. Possible values: "DESIGN", "DOCUMENTATION", "SECURITY", "OVERALL_SCORE". The default value is the "OVERALL_SCORE".</td>
      <td>no</td>
    </tr>
    <tr>
      <td rowspan= "3">Multipart/form-data</td>
      <td>File</td>
      <td>Compressed folder ZIP file. It must have the required structure.</td>
      <td>yes</td>
    </tr>
    <tr>
      <td>isVerbose</td>
      <td>Boolean attribute that activates the debug mode.</td>
      <td>no</td>
    </tr>
    <tr>
      <td>validationType</td>
      <td>Scoring module that the microservice evaluates. Possible values: "DESIGN", "DOCUMENTATION", "SECURITY", "OVERALL_SCORE". The default value is the "OVERALL_SCORE".</td>
      <td>no</td>
    </tr>
  </tbody>
</table>


{: .note}
You can check this API specification in the [API Scoring Engine repository](https://github.com/InditexTech/api-scoring-engine/tree/main/packages/certification-service/code/api_spec ).