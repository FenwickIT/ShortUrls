![logo](doc/logo.png)

[![GitHub license](https://img.shields.io/github/license/bhdicaire/vanityURLs)](https://github.com/bhdicaire/vanityURLs/blob/main/LICENSE) [![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](code_of_conduct.md) [![All Contributors](https://img.shields.io/badge/all_contributors-3-orange.svg?color=ee8449&style=flat-square)](#contributors)

vanityURLs is a _simple_ solution to deploy a budget-friendly Url Shortener. It runs at scale in your Cloudflare subscription with continuous integration.

> If you don't own an a Cloudflare subscription already, you can create your free account today so you can experience everything without spending a dime.

Features:
 * Fully branded internet domain using Cloudflare,  [DNS](https://www.cloudflare.com/en-ca/application-services/products/dns/) & [Pages](https://pages.cloudflare.com/) so your links are compact and pretty
 * URL redirection (301, 302, 303, 307 and 308)
 * Advanced redirection with splats (e.g., /news/*  &#8594; /blog/:splat )
 * Continuous integration managed by Cloudflare Page Engine

My objective is to work at the command line and automate it. So feel free to fork, and customize.

## What problem does it solve and why is it useful?

You’ve been there too, a fully branded short URLs is useful but your low volume does not justify a commercial solution. Furthermore, links generated by a free solution will eventually expire and they're not privacy friendly.

This kind of solution is known as TinyURL, tiny url, shorten that long URL, URL Shortening Service,  goo.gl, bit.ly, short.io, etc.

### It's bullet proof

As long as you secure your Github and Cloudflare accounts with robust authentication, there is not much that can go wrong with such simple solution. It use the products as designed, there is no hack involved. Refer to [Everything you always wanted to know about URL redirection (but were afraid to ask)](doc/url-redirection.md) for more information.

## Installation

1. Register a _tiny_ internet domain name with your [preferred vendor](https://www.cloudflare.com/en-ca/products/registrar/)
2. Add the domain to [Cloudflare DNS](https://dash.cloudflare.com/)
3. Fork the repository as a public or as a __private__ GitHub repository
4. Create a project underneath Cloudflare Workers & Pages
    *  [Connect the repository](https://developers.cloudflare.com/pages/get-started/guide/#connect-your-git-provider-to-pages)
    * Configure your deployment and build setup:
      * Framework preset: none
      * Build command: none
      * Build output directory: /build
    * Open the _xyz_.page.dev in your browser, you should be redirected to https://BHDicaire.com based on the current content of
    Setup a [custom domain](https://developers.cloudflare.com/pages/platform/custom-domains/) for your page project
5. Configure the DNS entry via [Cloudflare DNS](https://dash.cloudflare.com/)

## Administration

You can use the following `Bash scripts`, if this is your cup of tea. Refer to the [documentation](doc/administration.md).

| Name | Description |
| ---- | ----------- |
| `bin/lnk` | Generate a custom ID for a new URL, git add + commit |
| `bin/tinylnk` | Generate a unique ID for a new URL, git add + commit |


## How does it work?
The secret sauce are two plain text files:
  * `build/_redirects` based on this [documentation](https://developers.cloudflare.com/pages/platform/redirects)
  * `build/_headers` based on this [documentation](https://developers.cloudflare.com/pages/platform/headers/)

Make sure to put all the items with placeholders or splats at the end of the `build/_redirects`.

```bash
/mail https://outlook.office.com/ 301
/github https://github.com/bhdicaire/ 301
/github/* https://github.com/bhdicaire/:splat
```

> Pages uses HTTP validation and needs to hit an HTTP endpoint during validation. If another Cloudflare product is in the way (such as Access, a redirect, a Worker, etc.), validation cannot be completed.

I'm using the `build/_headers` to include the following items to Cloudflare Pages responses, don't forget to change the URLs for pages.dev and your custom domain:
```html
https://xyz.pages.dev/*
  X-Robots-Tag: noindex
  X-Content-Type-Options: nosniff

https://example.com/*
  X-Robots-Tag: noindex
  X-Content-Type-Options: nosniff
```



## Contributions

[Contributions](doc/CONTRIBUTING.md) are welcome! We recognize [all types](https://allcontributors.org/docs/en/emoji-key) based on the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Please note that this project is released with a [Contributor Code of Conduct](doc/CODE-OF-CONDUCT.md). By participating in this project you agree to abide by its terms.

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="16.66%"><a href="https://github.com/bhdicaire"><img src="https://avatars.githubusercontent.com/u/1316765?v=4?s=100" width="100px;" alt="Benoît H. Dicaire"/><br /><sub><b>Benoît H. Dicaire</b></sub></a><br /><a href="https://github.com/bhdicaire/vanityURLs/commits?author=bhdicaire" title="Code">💻</a> <a href="https://github.com/bhdicaire/vanityURLs/commits?author=bhdicaire" title="Documentation">📖</a> <a href="#security-bhdicaire" title="Security">🛡️</a></td>
      <td align="center" valign="top" width="16.66%"><a href="http://felixleger.com"><img src="https://avatars.githubusercontent.com/u/7781739?v=4?s=100" width="100px;" alt="Félix Léger"/><br /><sub><b>Félix Léger</b></sub></a><br /><a href="#ideas-felleg" title="Ideas, Planning, & Feedback">🤔</a> <a href="#userTesting-felleg" title="User Testing">📓</a> <a href="#promotion-felleg" title="Promotion">📣</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

## Related
 * [dnsConfiguration](https://github.com/bhdicaire/dnsConfiguration) – Automated DNS configuration with StackOverflow's DNSControl and Git

## Licence
**vanityURLs** is Copyright 2023 Benoît H. Dicaire and [licensed under the MIT licence](https://github.com/bhdicaire/vanityURLs/blob/master/LICENCE).
