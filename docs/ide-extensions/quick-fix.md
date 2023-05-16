---
layout: default
title: Quick Fix
parent: IDE Extensions
nav_order: 2
---

# Spectral quick fix
{: .no_toc }

The extension that focuses on establishing a ruleset file where you can find the compromised rule and fix it.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


When using Spectral for linting OpenAPI contracts, we encountered that it doesn’t suggest any quick fix for the linted error. So that is how this extension started.

{: .note}
Since this extension is based on Spectral, the Quick fix **only works for OpenAPI contracts**.

## Settings

This extension does not need any settings. Just download it and start enjoying it 😎

## Usage

To use it, open an API contract on VS Code, and if it has errors or warnings, your code will have **underlined text**. This happens because Spectral founds issues on your contract that break the API guidelines.

To **correct the warnings/errors**, put the cursor above the highlighted text, and you will see a tooltip with all the possible corrections that can be done - you can add, modify, or delete code.

If you **click on one of the options**, you quickly fix the code. Nice and easy.

![gif](/ide-extensions/quick-fix-gif.gif)