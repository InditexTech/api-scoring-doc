---
layout: page
title: Home
permalink: /
nav_order: 1
description: The API Scoring Suite is a compound of tools that make your journey of designing an API much more easy.
---

# Optimize your APIs with the **API Scoring Suite**
{: .fs-9 }

This open-source API-First-based Scoring service evaluates your APIs according to a set of rules that the user can customize.
{: .fs-6 .fw-300 }

[Get started now](#get-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[View it on GitHub](/github-repositories){: .btn .fs-5 .mb-4 .mb-md-0 }

---

The **API Scoring Suite** is a set of tools that can help you to achieve the best API you can get. It is made of the following components:
{: .mb-7}

<table>
  <thead>
    <tr>
      <th style="color:#6852D0;">Component</th>
      <th style="color:#6852D0;">Subcomponent</th>
      <th style="color:#6852D0;">Functionality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan= "4">Scoring system</td>
      <td>Microservice</td>
      <td>The main piece that <strong>certifies an API</strong> with a grade according to a certain set of rules. It gives you an overall score according on how well design is your API.</td>
    </tr>
    <tr>
      <td>Rulesets</td>
      <td>The set of rules that <strong>nourishes the scoring service</strong>. They can be customized or changed by a new set.</td>
    </tr>
    <tr>
      <td>API</td>
      <td>The <strong>entrance gate</strong> to the microservice. Its endpoints are used by the scoring tools like the CLI or the extensions.</td>
    </tr>
    <tr>
      <td>CLI</td>
      <td>The command line tool that helps you to easily get an <strong>instant result of your API's scrore</strong> from you terminal. You can also display which are the rules that have been compromised with a verbose command.</td>
    </tr>
    <tr>
      <td rowspan= "2">IDE Extensions</td>
      <td>API Hub</td>
      <td>This extension, along with a local SPA, is able to retrieve a <strong>visual and interactive review of your API's design</strong>.</td>
    </tr>
    <tr>
      <td>Quick Fix</td>
      <td>It allows you to instantly <strong>correct any rule breach with a click</strong>. This extension is able to remove or add new content to you API specification file.</td>
    </tr>
  </tbody>

</table>

## Demo
{: .mb-3}

{: .warning}
TO DO

## Get started 
{: .mb-3}

Let's start and see how you can build the whole ecosystem up!

1. Firs of all, you need to **deploy the microservice**. To do so, follow the [Microservice installation guide](/scoring-system/microservice/#installation).

2. Test the microservice by [Installing the CLI](/scoring-system/cli/#installation-and-usage). Test any API you have in hand!

3. Once you've verified that the microservice is up and running, you can now [deploy the SPA](/ide-extensions/overview/#spa-deployment) that the API Hub extension will use later on.

4. [Install the API Hub](/ide-extensions/overview/#installation) in VS Code or IntelliJ and [configure it](/ide-extensions/api-hub/#settings) to work with the scoring service.

5. [Install the Quick Fix](/ide-extensions/overview/#installation) to design faster!

## About the project
{: .mb-3}

API Scoring suite is &copy; 2023-{{ "now" | date: "%Y" }} by [Inditex Tech](https://github.com/InditexTech).

### License
{: .mb-3}

The **API Scoring Suite** is distributed by an [Apache License 2.0](https://github.com/InditexTech/api-scoring-engine/blob/main/LICENSE).

### Contributing
{: .mb-3}

When contributing to this repository, please first discuss the change you wish to make via issue,
email, or any other method with the owners of this repository before making a change. Read more about becoming a contributor in the [CONTRIBUTING](/contributing/) section.

#### Thank you to the contributors of Just the Docs!

<ul class="list-style-none">
{% for contributor in site.github.contributors %}
  <li class="d-inline-block mr-1">
     <a href="{{ contributor.html_url }}"><img src="{{ contributor.avatar_url }}" width="32" height="32" alt="{{ contributor.login }}"></a>
  </li>
{% endfor %}
</ul>

### Code of Conduct

Just the Docs is committed to fostering a welcoming community.

[View our Code of Conduct](https://github.com/just-the-docs/just-the-docs/tree/main/CODE_OF_CONDUCT.md) on our GitHub repository.

----

[^1]: The [source file for this page] uses all three markup languages.

[^2]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).

[Jekyll]: https://jekyllrb.com
[Markdown]: https://daringfireball.net/projects/markdown/
[Liquid]: https://github.com/Shopify/liquid/wiki
[Front matter]: https://jekyllrb.com/docs/front-matter/
[source file for this page]: https://github.com/just-the-docs/just-the-docs/blob/main/index.md
[Just the Docs Template]: https://just-the-docs.github.io/just-the-docs-template/
[Just the Docs]: https://just-the-docs.github.io/just-the-docs/
[Just the Docs README]: https://github.com/just-the-docs/just-the-docs/blob/main/README.md
[GitHub Pages]: https://pages.github.com/
[Template README]: https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md
[GitHub Pages / Actions workflow]: https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/
[use the template]: https://github.com/just-the-docs/just-the-docs-template/generate