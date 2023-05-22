---
layout: default
title: Rulesets
parent: Scoring System
nav_order: 2
---

# Rulesets
{: .no_toc }

TO DO
{: .fs-6 .fw-300 }


## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

<br>

## Default rules in the microservice

### AsyncAPI
`itx-spectral.yaml`

| Rule | Description |
| --	| -- |
| contact-email | Definition must have a contact email |
| contact-url | Contact email should be a valid URI |
| mandatory-description | Description must be present |
| must-use-semantic-versioning | Version must be in semver |


---

### Avro
`itx-spectral.yaml`

| Rule | Description |
| --	| -- |
| field-name-snake_case | All field names must match snake case pattern (e.g. snake_case) |
| fields-doc | Definition `doc` must be present and non-empty string in all fields |
| global-doc | Definition `doc` must be present and non-empty string in all types |
| type-name-pascal-case | All type names must match PascalCase pattern |

---


### Documentation

`/markdownlint/linting-rules/api-rules/`

| Rule | Description |
| --	| -- |
| api-mandatory-about |	About section is mandatory|

---


### OpenAPI - REST

`itx-spectral.yaml`

| Rule | Description |
| --	| -- |
| contact-email | Definition must have a contact email |
| contact-url	| Contact email should be a valid URI |
| ensure-operations-summary | Put a summary in all operations |
| openapi-version | OpenAPI version cannot be 3.1.X for the time being |

<br>

`security-spectral.yaml`

| Rule | Description |
| --	| -- |
| array-required-properties | Array size should be limited to mitigate resource exhaustion attacks. This can be done using `maxItems` |

<br>

`rulesets/api-versions.yaml`

| Rule | Description |
| --	| -- |
|must-use-semantic-versioning | All the API will be versioned following the Semantic Versioning definition |

<br>

`rulesets/examples.yaml`

| Rule | Description |
| --	| -- |
| components-param-examples | Componente parameters must have examples |
| ensure-properties-examples | Properties must have examples, description and type |
| paths-param-examples | Parameters must have examples |

<br>

`http-status-code.yaml`

| Rule | Description |
| --	| -- |
| delete-http-status-codes-resource | Each endpoint need to have defined the error codes |
| error-response-definitions | Define errors in your API following our version of the Problem Details RFC7807 |
| error-response-definitions-rfc7807-status	| Define errors in your API following our version of the Problem Details RFC7807 |
| get-http-status-codes-collections | Each endpoint need to have defined the error codes |
| get-http-status-codes-resource | Each endpoint need to have defined the error codes |
| patch-http-status-codes-resource | Each endpoint need to have defined the error codes	 |
| post-http-status-codes-collections | Each endpoint need to have defined the error codes |
| post-http-status-codes-controller | Each endpoint need to have defined the error codes |
| post-http-status-codes-resource | Each endpoint need to have defined the error codes |
| put-http-status-codes-resource | Each endpoint need to have defined the error codes |
| standard-http-status-codes | MUST use standard HTTP status codes |
| well-understood-http-status-codes	 | HTTP response codes cannot be used on all HTTP verbs |

<br>

`path.yaml`

| Rule | Description |
| --	| -- |
| path-parameters-camel-case | Path parameters should be camelCase |
| paths-no-underscore| Paths should not contain underscores |
| paths-uppercase	| Paths should not be in uppercase |
| query-camel-case| Query parameters should be camelCase |

<br>

`properties.yaml`

| Rule | Description |
| --	| -- |
| camel-case-for-properties | Use camelCase naming for attributes in request/responses and definitions |
| dto-schema-name | You SHOULD avoid ending your schemas (..schemas[*]~) with suffixes like {dto,DTO,Dto} |

<br>

`security.yaml`

| Rule | Description |
| --	| -- |
| allowed-auth-methods | The API operation uses HTTP authentication method that is not included in IANA Authentication Scheme Registry |
| allowed-verbs | Use always HTTP verbs to refer to actions in urls |
| array-required-properties | Array size should be limited to mitigate resource exhaustion attacks. This can be done using `maxItems` |
| empty-schema | The schema is empty. This means that your API accepts any JSON values. Or payload does not have any properties defined |
| empty-schema-headers | Define schemas for all header objects to restrict what input or output is allowed |
| ensure-auth | Authentication SHOULD support Basic and Bearer type |
| ensure-security-schemes | The security field of your API contract does not list any security schemes to be applied |
| global-security | Use the security field on the global level to set the default authentication requirements for the whole API |
| implicit-grant-oauth2 | Do not use implicit grant flow in OAuth2 authentication |
| negotiate-auth | Do not use the security scheme negotiateAuth |
| no-additional-properties-defined	 | While forbidding additionalProperties can create rigidity and hinder the evolution of an API - eg making it hard to accept new parameters or fields. It is possible that this flexibility can be used to bypass the schema validator and force the application to process unwanted information |
| numeric-required-properties-max-min	 | Numeric values should be limited in size to mitigate resource exhaustion |
| oauth1-auth | One or more global security schemes in your API allows using OAuth 1.0 authentication |
| resource-owner-password-auth | The API operation uses resource owner password grant flow in OAuth2 authentication |
| response-schema-defined | You have not defined any schemas for responses that should contain a body. Only acceptable if the returned HTTP status code is 204 or 304 (no content allowed for these codes), see RFC 7231 and RFC 7232 |
| schema-mandatory-parameters | One or more parameters in your API do not have schemas defined. All parameters must have either schema or content defined to restrict what content your API accepts|
| security-empty | One or more of the objects defined in the global security field contain an empty security requirement |
| security-scopes-defined | OAuth2 security requirement requires a scope not declared in the referenced security scheme |
| server-https | Set all server objects to support HTTPS only so that all traffic is encrypted |
| string-parameters-required-maxLength | String should be limited and with a maxLength to avoid out of format inputs by attackers |
| string-properties-required-maxLength | String should be limited and with a maxLength to avoid out of format inputs by attackers |



---
												
### Proto

| Rule | Description |
| --	| -- |												
| response-schema-not-defined | You have not defined any schemas for responses that should contain a body. Only acceptable if the returned HTTP status code is 204 or 304 (no content allowed for these codes), see RFC 7231 and RFC 7232 |