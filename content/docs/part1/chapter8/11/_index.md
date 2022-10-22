---
weight: 11
title: "8.11 Content plugins"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.11 Content plugins

Template plugins are useful abstractions over template code that we can reuse. Hugo Modules also allows us to have content plugins that can package content that we can reuse across multiple websites.

One example of content shareable across numerous websites is the Terms of Use and the Privacy Policy pages. Websites from the same company share the same Terms of Use page. We can move this page to an independent module and import it across all company websites for reuse. The page can use the built-in param function to access site parameters from the configuration and can also bundle shortcodes to provide standardized data across the multiple websites.

We need the same Terms of Use and the Privacy Policy pages across all websites under the Acme umbrella. The Terms of Use and the Privacy Policy pages for the Acme Corporation website are also present in the repository in github.com/hugoinaction/ TermsAndPrivacy   (https://github.com/hugoinaction/hugoinaction/tree/chapter-08-resources/06). The menu entries are in the front matter, and the hardcoded data values, which can differ across various websites, are replaced with the param shortcode (for example, {{&lt; param "TermsAndPrivacy.company_name" &gt;}} for the company name). Performing these changes has been left as an exercise for the reader.

![Figure8.4](Figure8.4.svg)

Figure 8.4 Months of work: Bob faces the brunt of the angry marketing head for not having a central place to keep the Terms of Use and Privacy Policy pages, which puts the marketing campaign at risk legally with the older Terms of Use.

We will integrate a plugin into the Acme Corporation website (and not the Acme Corporation theme) and configure it to get rid of our hardcoded Terms of Use and Privacy Policy pages. To integrate this plugin into the Acme Corporation website, we will need to perform the following steps.
- 1 Delete the terms.md and the privacy.md pages.
- 2 Update the module.yaml file in the config/_default folder with the contents in the   following   listing   (https://github.com/hugoinaction/hugoinaction/tree/ chapter-08-resources/07).

{{< details title="Listing 8.11 Adding a new dependency (config/_default/module.yaml)" open=true >}}
```yaml
imports:
  - path: github.com/hugoinaction/TermsAndPrivacy
...
```
{{< /details >}}

- 3 Add the terms and privacy parameters to the configuration for the TermsAndPrivacy repository as the following listing shows.

{{< details title="Listing 8.12  Adding the parameters (config/_default/params.yaml)" open=true >}}
```yaml
TermsAndPrivacy:
  company_name: Acme Corporation 
  contact_email: contact@example.org 
  website: https://hugoinaction.com 
  contact_dpo_email: dpo@hugoinaction.com 
  contact_dpo_phone: 9999999999
```
{{< /details >}}

- 4 Add the menu file to bring back the footer menu entries as the following listing shows.

{{< details title="Listing 8.13 Restoring the footer entries (config/_default/menu.yaml)" open=true >}}
```yaml
footer:
    - name: Privacy Policy
      weight: 300
      url: /privacy
    - name: Terms of Use
      weight: 200
      url: /terms
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-09.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-09.
{{< /hint >}}

The Privacy Policy and the Terms of Use pages load from a shared content module with these changes. This module is generic, and you are free to use this for your own websites outside of Acme Corporation and Hugo in Action.

{{< hint info >}}
**Exercise 8.3**

Which of the following is an accurate statement about a content plugin? (Select all that apply.)
- a. A content plugin creates a link to the shared content in the generated website.
- b. A content plugin cannot have template code.
- c. A content plugin can be used to set up access control on the content by splitting each area into a separate repository.
- d. A content plugin moves the common content into a separate repository for one place of access.
{{< /hint >}}