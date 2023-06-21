---
layout: default
title: API Hub
parent: IDE Extensions
nav_order: 1
---

# API Hub
{: .no_toc }

A tool that establishes communication between a scoring web and the files of the IDE.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

This extension emerges from the need for a tool that combines the power of the scoring service and the power of IDEs.

This web can be used as a web itself or integrated into the IDE through an iFrame format.

This extension works by sending a ZIP file with the repository to the web service, which obtains a grade. This web can display errors and warnings by linting the APIs and displaying different grades. Coming back to the file and correcting the mistakes can be done by clicking the error/warning on the iFrame, so the communication is bidirectional.

Once you update the linted errors, you can press play on the iFrame and see the new grade because a new grade was triggered with the updated file.

## Settings

To start using the API hub extension, you need to configure two URLs in the **APIHub Settings**:
- The `Certification URL` needs to be set to the URL where the [scoring service](/scoring-system/microservice/) is deployed. The default value is `http://localhost:8080/apifirst/v1/apis/validate`.
- The `Frontend URL` has to be set to the URL where the [SPA](/ide-extensions/overview/#spa-deployment) is deployed. The default value is `http://localhost:3000/`.

## Usage
{: .mb-3}

{: .highlight}
> To start using this extension, you need to:
> 1. Deploy the [Scoring service](/scoring-system/microservice/).
> 2. Deploy the [SPA](#spa-deployment).
> 3.  [Install](#%EF%B8%8F-installation) it.


1. Open a repository in VS Code that contains a `metadata.yml` file with the following structure:

    ```yml
    apis:
    - name: # The API name
       api-spec-type:   # API type: grpc, event, rest
       definition-path: # Path to API folder
       definition-file: # API definition file
    ```

    {: .note}
    You can customize the file and add as many APIs and specifications as you want!

2. Click on the API 360 Certification button on the right-bottom corner of the VS Code window. This action will display a web server on a VS Code tab.
   
   <p align="center">
   <img src="/ide-extensions/buttons.png" style="display: block; width: 300px; margin-left: auto; margin-right: auto; padding-top:10px; padding-bottom:10px"/>
   </p>

3. Check out how well-designed your API is through the scores obtained by the scoring service.

4. Go to the linted errors by clicking on the **Rule break line link**, and correct them for a better score!

    - Remember that you can use the [Spectral quick fix](#spectral-quick-fix) to make this step so much easier!

5. Once you have made the changes, **save the file**, go back to the iFrame, and click the re-run button. This will make the service analyze the **module** again.

6. If you want to re-calculate the **overall** score of the API, you can whether:
  - click on the upper play button.
  - close the iFrame and re-open it as it was made in _Step 2_.

## Repository scoring

When you open the iFrame, the following view is displayed:
   <p align="center">
      <img src="/ide-extensions/iFrame.png" style="display: block; width: 450px; margin-left: auto; margin-right: auto; padding-top:10px; padding-bottom:10px"/>
   </p>

All the APIs that exist in the repository are going to be shown as tabs. Each API gets a score individually, and you can switch between them to see which are the warnings for each of them.

Every API is scored with four grades: One grade for each module (Design, Security, and Documentation) and the other for the overall. To know how the scoring is performed, check out the Scoring criteria.

## File validation

For the Visual Studio Code extension, there is also another button, the _APIHub File Lint_, next to the _APIHub_.

Clicking on the _API 360 Linter_ button will display a new window in which you can select a file that contains your custom rules.

<!-- [Validate file view - todo](todo) -->

With this new functionality, you can lint any file with your custom rules!

To certify with a custom YML file, you should:

1. Create one YML file following [these guidelines](https://meta.stoplight.io/docs/spectral/e5b9616d6d50c-custom-rulesets).

2. Place the custom ruleset in the correct place, following this structure:

   ```
   ├── file-rules
   │   ├── <ruleset_name>
   │       └── itx-spectral-ruleset.yml
   ```

{: .note}
Notice that you can add Javascript functions to the YAML file, which will enrich the power of your ruleset!