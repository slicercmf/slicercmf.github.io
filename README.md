# slicercmf.github.io

Infrastructure for generating the content of the SlicerCMF website published at https://cmf.slicer.org

## Automatic deployment

The site is generated using the static site generator Jekyll and is automatically deployed as GitHub pages
each time the `master` branch is updated.

For more details, see https://jekyllrb.com/docs/github-pages/

## Local development

This requires ruby, bundler and jekyll.

It is possible to install ruby and relevant packages by following these [detailed instructions](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll) published by GitHub.

An easier approach is to use the docker image [Starefossen/docker-github-pages](Starefossen/docker-github-pages).

These instructions allows to locally build the site and make it available at http://localhost:4000. Any changes
to the sources will be detected and the site will be locally rebuilt.

1. Download docker image

    ```
    docker pull starefossen/github-pages
    ```

2. Download website sources

    ```
    git clone git://github.com/slicercmf/slicercmf.github.io
    ```

3. Shell into the container

    ```
    cd slicercmf.github.io
    docker run   -ti --rm   -v "$PWD":/usr/src/app -p "4000:4000" starefossen/github-pages sh
    ```

4. Locally build and serve the site at http://localhost:4000

    ```
    jekyll serve -d /_site --watch --force_polling -H 0.0.0.0 -P 4000 --incremental
    ```

## Mapping with the `cmf.slicer.org` domain

The mapping is enabled by (1) the [CNAME][CNAME] file added to the root of the repository and (2) configuration
of the DNS associated `slicer.org`.


## Why this repository is not in the DCBIA-OrthoLab GitHub organization ?

Considering that there are two types of site served as GitHub pages:
* User or organization site served as `https://username.github.io` or `https://organization.github.io`
* Project site served as `https://username.github.io/repository` or `https://organization.github.io/repository`

and considering that the custom domain will replace the `username.github.io` or `organization.github.io` portion
of the URL, we created a dedicated site for the `slicercmf` user to allow use of custom domain  without having the
extra `/repository`.

Note that we could have created a project called `https://github.com/DCBIA-OrthoLab/DCBIA-OrthoLab.github.io` but we
wanted to keep that option open for managing a site dedicated to the lab.

For more details, see:
* [About custom domains and GitHub Pages](https://help.github.com/en/github/working-with-github-pages/about-custom-domains-and-github-pages#supported-custom-domains)
* [Configuring a custom domain for your GitHub Pages site](https://help.github.com/en/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site)
