---
layout: default
title: CLI
parent: Scoring System
nav_order: 4
---

# Scoring **CLI**
{: .no_toc }

With `apicli`, you can make requests to the scoring system and get your API a grade.
{: .fs-6 .fw-300 }

<br>

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Summary

Once you install this CLI, you will be able to:

* [x] Verify if an API is well-designed.
* [x] Verify an API contract specification (OpenAPI, AsyncAPI, Avro, Protobuf Buffer) or the respective documentation files (Markdown).

## Installation and usage

1. You can start by cloning [this repository](https://github.com/InditexTech/api-scoring-engine): 

    ```zsh
    git clone git@github.com:InditexTech/api-scoring-engine.git
    ```

2. Place yourself in the correct package: 

    ```zsh
    cd packages/api-cli/code
    ```

3. Install the downloaded code dependencies:  

    ```zsh
    npm i
    ```

4. Link the `apicli` command to local installation:  

    ```zsh
    npm link
    ```


## Comands

Then, you can use any of these commands: 

- `verify`, with which you can obtain the score of the API, all along with some helpful information like version numbers or protocol. 

- `verify-file`, verifies an OpenAPI specification file.
- general and command-dedicated `help`, in case you need further information.

### \> `verify` command
[(Back to top)](#top)
{: .fs-2 }

If you run the `apicli verify`command, you will get an output similar to the following example (verbose as default):


``` json
[
  {
    "validationDateTime": "2023-01-25T12:52:58.606Z",
    "apiName": "REST Sample",
    "apiProtocol": "REST",
    "result": [
      {
        "linterValidation": {
          "validationType": "LINTER",
          "spectralValidation": {
            "issues": [
              {
                "code": "ensure-operations-summary",
                "message": "Missing the get.summary",
                "path": ["paths", "/products", "get"],
                "severity": 1,
                "source": "/myApis/rest/contract/openapi-rest.yml",
                "range": {
                  "start": { "line": 19, "character": 8 },
                  "end": { "line": 128, "character": 54 }
                },
                "fileName": "/myApis/rest/contract/openapi-rest.yml"              }
            ]
          },
          "protolintValidation": { "issues": [] },
          "score": 98.7,
          "rating": "A",
          "ratingDescription": "Very Good"        }
      },
      {
        "securityValidation": {
          "validationType": "SECURITY",
          "spectralValidation": { "issues": [] },
          "protolintValidation": { "issues": [] },
          "score": 100,
          "rating": "A+",
          "ratingDescription": "Excellent"        }
      },
      {
        "documentationValidation": {
          "validationType": "DOCUMENTATION",
          "issues": [],
          "score": 100,
          "rating": "A+",
          "ratingDescription": "Excellent"        }
      }
    ],
    "score": 99.48,
    "rating": "A",
    "ratingDescription": "Very Good",
    "hasErrors": false  }
]
```

### \> `verify-file` command
[(Back to top)](#top)
{: .fs-2 }

To use the `verify-file` command, you need to retrieve an input file. For example, if you run the following input:

```bash
apicli verify-file --specificationFile=./apis/apicertification/rest/openapi-rest.yml
```

You will get the following output:

```json
{
    "hasErrors": false,
    "results": [
        {
            "code": "error-response-definitions-rfc7807-status",
            "message": "RFC-7807 Problem specification: status (integer) should be defined",
            "path": [
                "components",
                "schemas",
                "errorObject",
                "properties"
            ],
            "severity": 1,
            "source": "c:/Users/hnpz/AppData/Local/Temp/89107eb7ff2f22bc54f3e93cad88daf77b54613bcb5d7500/yaml-1673617840813.yaml",
            "range": {
                "start": {
                    "line": 695,
                    "character": 17
                },
                "end": {
                    "line": 722,
                    "character": 113
                }
            }
        },
        {
            "code": "error-response-definitions-rfc7807-status",
            "message": "RFC-7807 Problem specification: status (integer) should be defined",
            "path": [
                "components",
                "schemas",
                "400BadRequestError",
                "properties"
            ],
            "severity": 1,
            "source": "c:/Users/hnpz/AppData/Local/Temp/89107eb7ff2f22bc54f3e93cad88daf77b54613bcb5d7500/yaml-1673617840813.yaml",
            "range": {
                "start": {
                    "line": 734,
                    "character": 17
                },
                "end": {
                    "line": 740,
                    "character": 52
                }
            }
        },
        {
            "code": "error-response-definitions-rfc7807-status",
            "message": "RFC-7807 Problem specification: status (integer) should be defined",
            "path": [
                "components",
                "schemas",
                "401UnauthorizedError",
                "properties"
            ],
            "severity": 1,
            "source": "c:/Users/hnpz/AppData/Local/Temp/89107eb7ff2f22bc54f3e93cad88daf77b54613bcb5d7500/yaml-1673617840813.yaml",
            "range": {
                "start": {
                    "line": 752,
                    "character": 17
                },
                "end": {
                    "line": 758,
                    "character": 52
                }
            }
        },
        {
            "code": "error-response-definitions-rfc7807-status",
            "message": "RFC-7807 Problem specification: status (integer) should be defined",
            "path": [
                "components",
                "schemas",
                "403ForbiddenError",
                "properties"
            ],
            "severity": 1,
            "source": "c:/Users/hnpz/AppData/Local/Temp/89107eb7ff2f22bc54f3e93cad88daf77b54613bcb5d7500/yaml-1673617840813.yaml",
            "range": {
                "start": {
                    "line": 770,
                    "character": 17
                },
                "end": {
                    "line": 776,
                    "character": 52
                }
            }
        },
        {
            "code": "error-response-definitions-rfc7807-status",
            "message": "RFC-7807 Problem specification: status (integer) should be defined",
            "path": [
                "components",
                "schemas",
                "404NotFoundError",
                "properties"
            ],
            "severity": 1,
            "source": "c:/Users/hnpz/AppData/Local/Temp/89107eb7ff2f22bc54f3e93cad88daf77b54613bcb5d7500/yaml-1673617840813.yaml",
            "range": {
                "start": {
                    "line": 788,
                    "character": 17
                },
                "end": {
                    "line": 794,
                    "character": 52
                }
            }
        },
        {
            "code": "error-response-definitions-rfc7807-status",
            "message": "RFC-7807 Problem specification: status (integer) should be defined",
            "path": [
                "components",
                "schemas",
                "500InternalServerError",
                "properties"
            ],
            "severity": 1,
            "source": "c:/Users/hnpz/AppData/Local/Temp/89107eb7ff2f22bc54f3e93cad88daf77b54613bcb5d7500/yaml-1673617840813.yaml",
            "range": {
                "start": {
                    "line": 806,
                    "character": 17
                },
                "end": {
                    "line": 812,
                    "character": 52
                }
            }
        },
        {
            "code": "error-response-definitions-rfc7807-status",
            "message": "RFC-7807 Problem specification: status (integer) should be defined",
            "path": [
                "components",
                "schemas",
                "503ServiceUnavailableError",
                "properties"
            ],
            "severity": 1,
            "source": "c:/Users/hnpz/AppData/Local/Temp/89107eb7ff2f22bc54f3e93cad88daf77b54613bcb5d7500/yaml-1673617840813.yaml",
            "range": {
                "start": {
                    "line": 824,
                    "character": 17
                },
                "end": {
                    "line": 830,
                    "character": 52
                }
            }
        },
        {
            "code": "error-response-definitions-rfc7807-status",
            "message": "RFC-7807 Problem specification: status (integer) should be defined",
            "path": [
                "components",
                "schemas",
                "504GatewayTimeOut",
                "properties"
            ],
            "severity": 1,
            "source": "c:/Users/hnpz/AppData/Local/Temp/89107eb7ff2f22bc54f3e93cad88daf77b54613bcb5d7500/yaml-1673617840813.yaml",
            "range": {
                "start": {
                    "line": 842,
                    "character": 17
                },
                "end": {
                    "line": 848,
                    "character": 52
                }
            }
        }
    ]
}
```


