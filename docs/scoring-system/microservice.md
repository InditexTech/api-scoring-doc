---
layout: default
title: Microservice
parent: Scoring System
nav_order: 1
---

# Scoring service
{: .no_toc }

The microservice responsible for getting a grade for each API.
{: .fs-6 .fw-300 }

<br>

<div >
    <img src="/scoring-system/cert-image.png" width="20%" style="float: right;"> 
</div>

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

<br>

## Summary

API Scoring is the microservice responsible for getting a grade for each API. It has several modules to certify different aspects of each API and calculate a final score for them using a weighted average.

This open-source API-First-based scoring service evaluates your APIs according to a set of rules that the user can customize.

We want to make it simple. In the end, each certified API will be broken down into a single grade, which will mean how well-design your API is. 

If you want to know if your API complies with your design rules, if it addresses some of the OWASP vulnerabilities, and if it complies with documentation guidelines… this is your service.

{: .warning }
Due to an [issue in protolint](https://github.com/yoheimuta/protolint/issues/144), getting a score for gRPC APIs in Windows it is not possible.

## Installation

Know that we recommend the use of [Node v18.13.0](https://nodejs.org/es/blog/release/v18.13.0/) to work on this project. 

Deploy the service following these steps: 

1. Clone [this repository](https://github.com/InditexTech/api-scoring-engine):

    ```zsh
    git clone git@github.com:InditexTech/api-scoring-engine.git
    ```

2. Place yourself in the correct package: 

    ```zsh
    cd packages/certification-service/code/
    ```

3. Install the dependencies: 

    ```zsh
    npm i
    ```

4. Optionally, add your GitHub credentials one of the following ways to be able to validate private repositories:

   - as environment variables:

      ```zsh
      CERWS_GH_USERNAME # GitHub username.
      CERWS_GH_PASSWORD # GitHub personal access token.
      ```
   - or in the [`configmap.yml` file](https://github.com/InditexTech/api-scoring-engine/blob/main/packages/certification-service/code/config/configmap.yml):
      ```yml
      cerws:
        common:
          rest:
            client:        
              github-rest-client:
                username: <GITHUB_USERNAME>
                password: <GITHUB_PERSONAL_ACCESS_TOKEN>
      ```

5. Run the service: 

    ```bash
    npm start
    ``` 

<br>

You can make use of this service by just making a request to its [API](/scoring-system/api/) or, even better, using the [Scoring CLI](/scoring-system/cli/) tool that we have developed for this matter.
{: .mb-6}

You can also use the [IDE Extensions](/ide-extensions/overview/) to help you design your API at the same time you validate it with the service. The API hub provides the rating of the modules evaluated on the scoring service, giving you real-time insights into what score to expect.
{: .mb-4}

{: .highlight}
You can check the **available enpoinds** in the [API](/scoring-system/api/) section.

## Performance and configuration
{: .mt-8}

As you have previously read, the microservice works with a compound of rules that come by default in the [Rulesets repository](https://github.com/InditexTech/api-scoring-engine/blob/main/packages/certification-service/code/src/rules).
{: .mb-4}

### Scoring
{: .fs-5}

In order to give meaningful feedback to the users while evaluating their APIs, API Scoring system serves a grade from *A<sup>+</sup>* to *D*, so developers can have a rating scale to refer to know the aspects that compromise their APIs and how to improve them.

Since Spectral, markdownlint, and protolint use a similar engine, we have defined a mechanism that works in the same fashion for the Design, Security, and Documentation modules.


#### **Criteria**
{: .mb-2 .mt-7 .fs-3}

The scoring system for each component will follow the previously mentioned *letter-based grade* system and:

* Each module is individually scored.
* The score for each module starts at the maximum value, namely 100 (A<sup>+</sup>).
* The final score is a weighted average of the modules that apply.
* For each type of broken rule, a specific number of points is deducted from the score.
* There are three kinds of rules: errors, warnings, and information. This latter kind does not decrease the grade anyhow.
* Designers can consult which rules have been broken using the [API 360 hub extension](/ide-extensions/api-hub/), so they know how to improve them.
{: .mb-7}

| Score | Letter |
|:---:|:---:|
|100|A<sup>+</sup>|
|90 - 99|A|
|75 - 89|B|
|50 - 74|C|
|0 - 49|D|

To obtain the final score of an API, the microservice considers every *individually-certified* module and operates according to a **weighted average**.
{: .mt-8}

{: .highlight}
Notice that not every module is supported by every protocol. Remember that **Security is only supported for REST**, while Design and Documentation are supported for REST, Event, and gRPC. GraphQL is not supported for the moment.


<p class="text-center fs-5 mt-6">Three modules approach</p>

<table>
  <thead>
    <tr> 
      <th colspan="2">Module</th>
      <th colspan="2">Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2">Design</td>
      <td colspan="2" style="text-align: center;">0.4</td>
    </tr>
    <tr>
      <td colspan="2">Security</td>
      <td colspan="2" style="text-align: center;">0.45</td>
    </tr>
    <tr>
      <td rowspan="2">Documentation</td>
      <td rowspan="2">0.15</td>
      <th>Convention rules</th>
      <td>0.30</td>
    </tr>
    <tr>
      <th>Custom rules</th>
      <td>0.70</td>
    </tr>
  </tbody>
</table>


<p class="text-center fs-5 mt-8">Two modules approach</p>

<table>
  <thead>
    <tr>
      <th colspan="2">Module</th>
      <th colspan="2">Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2">Design</td>
      <td colspan="2" style="text-align: center;">0.85</td>
    </tr>
    <tr>
      <td colspan="2">Security</td>
      <td colspan="2" style="text-align: center;">N/A</td>
    </tr>
    <tr>
      <td rowspan="4">Documentation</td>
      <td rowspan="4">0.15</td>
      <th>Convention rules</th>
      <td>0.30 </td>
    </tr>
    <tr>
      <th>Custom rules</th>
      <td>0.70</td>
    </tr>
  </tbody>
</table>

#### **Design and Security modules**
{: .mb-2 .mt-9 .fs-3}

The Design and Security modules' grade is calculated the same way, according to the following formula:

<!-- $$ModuleGrade = \left(1 -\frac{Warnings}{TotalRules}-\frac{Errors}{TotalRules}* N\right) * 100$$ -->

<p align="center">
  <img src="/scoring-system/module-grade-1.png" style="display: block; width: 55%; margin-left: auto; margin-right: auto; padding-top:5px; padding-bottom:10px"/>
  <span class="fs-2">Figure 1. Module grade calculation.</span>
</p>


The score of these modules depends, as you see on the _Figure 1_, on the following values:

* `Warnings`: number of warning-type rules that broke.
* `Errors`: number of error-type rules that broke.
* `TotalRules`: number of rules within the module.
* `N`: Factor number that indicates de severity of the errors. By default, it is 5.

#### **Documentation module**
{: .mb-2 .mt-7 .fs-3}

As you can notice in the _Table 1_ and _2_, the documentation module has a 15% weight in the overall score, and, at the same time, it includes an inner weighted average.

* The Markdown convention rules weigh 30% of the documentation grade.
* The Markdown custom rules weigh 70% of the documentation grade.

Therefore, each rule's weight will be affected by an extra factor. You can check how this works in the xref:#example[expample] below.


#### **Overall**
{: .mb-2 .mt-7 .fs-3}

Once each module's grade is calculated, it is time to do the weighted average to get the final score. For this, you need to sum all the module's scores multiplied by their weight, i.e.:


<!-- $$OverallScore = DesignGrade * 0.4 + SecurityGrade * 0.45 + DocumentationGrade * 0.15
$$

$$OverallScore = DesignGrade * 0.85 + DocumentationGrade * 0.15
$$ -->

<p align="center">
  <img src="/scoring-system/overall-score-1.png" style="display: block; width: 95%; margin-left: auto; margin-right: auto; padding-top:5px; padding-bottom:10px"/>
  <span class="fs-2">Figure 2. Overall score calculation (3 modules approach).</span>
  <br><br>
  <img src="/scoring-system/overall-score-2.png" style="display: block; width: 73%; margin-left: auto; margin-right: auto; padding-top:5px; padding-bottom:10px"/>
  <span class="fs-2">Figure 3. Overall score calculation (2 modules approach).</span>
</p>


{: .note}
For the **Documentation module**, different weights are assigned base and custom rules. To calculate the Documentation module score, the service operates with a weighted average of the two kinds of rules.

Each module's rules can be whether warnings, errors, or information. The breach of each of them means:

- **Warning**: This is not compliant with the guidelines, or the contract is not fully documented, but it's still valid — they have a lower impact on grade.
- **Error**: Failures of this severity might severely impact the usage of this contract as the source of truth, or it's not valid at all — they have a higher impact on the grade.
- **Information**: Suggestions on how to improve your API documentation that doesn't mean it's poorly documented — They have **no impact on the grade**.

A correction factor is added for error-type rules breach, assigning them a higher weight.



### Customization
{: .mt-8}

You can **modify the score calculation** by adjusting some parameters in the [`configmap.yml` file](code/config/configmap.yml) :

- If you want to increase the weight of errors, you can increase the value of the `error-coefficient-weight` property, which by default is `5`.

- If you want to modify the weight of the modules, you can change them in the `modules-weights` and `modules-weights-without-security` properties to adjust them to your needs.

- You can also modify in the Documentation module the weights of the base and custom rules in `rules-weights`.

You can **modify the whole set of rules** in the `lint-repository-folder` property.  The default route is the set of rules in this repository, but you can change it to the Rulesets repository. 

Once you install and deploy the service as explained in the [⚙️ Installation section](#-installation), you can make a `POST` to the `{{baseUrl}}/rulesets/refresh` endpoint (with this request, the application will download the new ruleset to the `/src/rules` folder, overwriting the current rules):

    curl --location --request POST 'http://localhost:8080/apifirst/v1/rulesets/refresh'
<!-- todo: update localhost URL -->

* You can change the location where the rules are downloaded modifying the configuration file:

  ```yml
  cerws:
    common:
      rest:
        client:
          github-rest-client:
            lint-repository-folder: "/src/rules"
  ```

  * If you modify this path you will need to update the following properties to update their paths too:

    ```yml
    cerws:    
      lint:    
        rest:
          general-default-ruleset: # Path of the file with the rules that will be applied in the linting of rest APIs
          security-default-ruleset: # Path of the file with the rules that will be applied in the security linting of rest APIs
        event:
          general-default-ruleset: # Path of the file with the rules that will be applied in the linting of async APIs
        avro:
          general-default-ruleset: # Path of the file with the rules that will be applied in the linting of async APIs with Avro
        grpc:      
          configuration-directory: # Path of the protolint configuration 
          severities-file:  # Path of the configuration file with the severity of the violations for grpc rules (by default the severity is warn)
      markdown:    
        markdown-lint-config: # Path of the markdownlint configuration file 
        markdown-lint-api-custom-rules: # File path with custom markdownlint rules 
    ```
* You can also use the [apicli](/scoring-system/cli/) tool to update the rulesets with the [Rulesets](link) repository with a CLI command.


### New rules creation
{: .mt-8}

The scoring rules are based on different linters depending on the files that are linting. If you want to create your own rules, you should follow each linter's documentation:

- For OpenAPI/AsyncAPI, follow [Spectral documentation](https://docs.stoplight.io/docs/spectral/01baf06bdd05a-create-a-ruleset).
- For documentation files, follow [markdownlint documentation](https://github.com/DavidAnson/markdownlint/blob/main/doc/CustomRules.md).
- For gRPC, follow [protolint documentation](https://github.com/yoheimuta/protolint/tree/d19308920340bcaf80064c65d24a818d12b3fb71#creating-your-custom-rules).