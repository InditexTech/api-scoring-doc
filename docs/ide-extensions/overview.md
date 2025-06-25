---
layout: default
title: IDE Extensions
nav_order: 3
has_children: true
---
<!--
SPDX-FileCopyrightText: 2023 Industria de Diseño Textil S.A. INDITEX

SPDX-License-Identifier: Apache-2.0
-->

# IDE Extensions
{: .no_toc }

The set of extensions that integrates the API-design essential tools into their everyday work.
{: .fs-6 .fw-300 }

<div align="center">
    <img src="../quick.svg" width="100px" style="margin-right: 30px">
    <img src="../api-hub-logo.svg" width="100px" style="margin-right: 30px">
</div>

<br>

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

<br>

## Summary

These set of extensions were built with a cooperation mindset between them: they increase the capabilities of each other, including [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) and [Spectral](https://marketplace.visualstudio.com/items?itemName=stoplight.spectral).

The [API hub](#api-hub) provides the rating of the modules evaluated on the [Scoring service](../../scoring-system/microservice/), giving you real-time insights into what score to expect. For every rule broken, you can easily open the respective file/line on your IDE! And it works with Visual Studio Code and IntelliJ.

To work, the API hub uses an in-IDE-integrated SPA, that displays visual information about the broken rules and uses bidirectional communication with your API files.

In the **VS Code**, you can take advantage of the [Spectral quick fix](#spectral-quick-fix) plugin to easily correct the linted errors. See in the previous gif how errors are corrected with a click!

<span class= "d-flex mt-5">
  [<img src="../../github-logo-gradient.png" width="30px" style="vertical-align: middle;"> Check the repository!](https://github.com/InditexTech/api-scoring-ide-plugins){: .btn .mx-auto  .mt-2 .mb-4}
</span>

{: .note}
For these tools to work, **you must deploy the Scoring microservice**: the main piece of the scoring system. Learn how in the [Scoring service section](../../scoring-system/microservice/).

## SPA deployment

You need to have the SPA running so that the extensions are working seamlessly. To do so, you need to deploy the SPA locally with the following commands:

1. Clone [this repository](https://github.com/InditexTech/api-scoring-ide-plugins):

    ```bash
    git clone git@github.com:InditexTech/api-scoring-ide-plugins.git
    ```


2. Navigate to the SPA directory:

    ```bash
    cd plugins/spa-apiscoringviewer/code
    ```


3. Install dependencies:

    ```bash
    npm install --global pnpm
    pnpm install
    ```


4. Once the process finishes, start the SPA:

    ```bash
    pnpm start
    ```

> [!TIP]
> If you need to remove all dependencies, you can use the following command:
>
> ```bash
> pnpm clean
> ```


## Installation

To install the extensions, follow the steps outlined below for each plugin.

### VSCode

1. Clone the repository:

    ```bash
    git clone git@github.com:InditexTech/api-scoring-ide-plugins.git
    ```

2. Install VSCE by following the official documentation [documentation](https://www.npmjs.com/package/@vscode/vsce), or use the command below::

    ```bash
    npm install --global @vscode/vsce
    ```

3. Navigate to `plugins/vscode-apiscoring/code` folder and run the following commands:

    ```bash
    npm install
    vsce package
    ```

4. The previous step will generate a `.vsix` file in the directory. Use this file to install the extension in VSCode.

    
### IntelliJ

1. Clone the repository:

    ```bash
    git clone git@github.com:InditexTech/api-scoring-ide-plugins.git
    ```

2. Build the plugin from `plugins/intellij-apiscoring/code`:

    ```bash
    ./gradlew build
    ```