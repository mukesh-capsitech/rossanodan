# Welcome to rossanodan 👋
[![Twitter: rossanodan](https://img.shields.io/twitter/follow/rossanodan.svg?style=social)](https://twitter.com/rossanodan)

> This repository contains my personal blog I built using [Hugo](https://gohugo.io/).

### 🏠 [Homepage](https://rossanodan.me/)

## Development notes

To scaffold the project it was enough to run the following commands

```bash
hugo new site rossanodan
cd rossanodan
git init
git submodule add https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

Once installed the [theme](https://github.com/dillonzq/LoveIt.git), I focused on customizing the `config.toml` file. It contains a long list of settings for the website like the title, social links and more.

```
baseURL = "https://rossanodan.me/"
defaultContentLanguage = "en"
languageCode = "en"
title = "rossanodan"

theme = "LoveIt"

[params]
  version = "0.2.X"
  description = "Rossano D'Angelo's personal website"
  keywords = ["Theme", "Hugo"]

...
```

I thought it was classy to buy a domain - not because I don't like the two free domains Firebase provides! - so I bought rossanodan.me on [GoDaddy](https://uk.godaddy.com/).

Setting up custom domains on Firebase is really easy and I also learnt a trick - thanks [Julien](https://twitter.com/BPS_Julien). Once set the custom domain, visit https://developers.google.com/speed/public-dns/cache and flush the cache. It gives you a little boost! :rocket:

I thought it was also fair to setup a CI workflow on GitHub Actions! Visit https://github.com/rossanodan/rossanodan/actions to see my workflow in action. Here's the `yml` file https://github.com/rossanodan/rossanodan/blob/master/.github/workflows/ci.yml.

## Author

👤 **Rossano D'Angelo**

* Website: https://dev.to/rossanodan
* Twitter: [@rossanodan](https://twitter.com/rossanodan)
* Github: [@rossanodan](https://github.com/rossanodan)
* LinkedIn: [@rossanodan](https://linkedin.com/in/rossanodan)