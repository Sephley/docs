# My personal documentation
This repository uses `mkdocs` with the `mkdocs-material` theme.

I will be documenting my notes from school modules here.

## Installation
- Create a GitHub repository
- Create the file `mkdocs.yml` in the root of your repository with the following content:
```
site_name: My MkDocs Website
theme:
    name: material
```
*note that this configuration only specifies a site & theme name. You can do a lot more though, see [**my current `mkdocs.yml` file.**](mkdocs.yml)*
- Create a directory called `docs` with a file called `index.md`. The contents of this file will be displayed on your website.
- Create the directories `.github/workflows` and add a file called `ci.yml` with the following content:
```
name: deploy website
on:
  push:
    branches:
      - master 
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV 
      - uses: actions/cache@v3
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache
          restore-keys: |
            mkdocs-material-
      - run: pip install mkdocs mkdocs-material 
      - run: mkdocs gh-deploy --force
```
*note that if you are using a different theme, you will need to replace the mkdocs-material theme with the one you are using.*  
- Enable GitHub pages in your repository settings | Make sure to deploy from the `gh-pages` branch from the `root` directory.

## Configuration
If you would like to edit for example the navigation bar, this can be configured in the `mkdocs.yml` file as stated in the [**official documentation.**](https://www.mkdocs.org/user-guide/configuration/)  
### Custom Domain
First of all, you must create the appropriate DNS records, as stated [**here.**](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)
Next add a file called `CNAME` to the branch you are deploying from, with the following contents:
```
example.domain.com
```

## Extensions
To use extensions such as these [**official markdown extensions**](https://python-markdown.github.io/extensions/), you can install `pymdown-extensions` with pip.  
If you would like to use some [**third-party exensions**](https://github.com/Python-Markdown/markdown/wiki/Third-Party-Extensions), you must install these separately.