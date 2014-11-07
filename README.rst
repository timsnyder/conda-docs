===================
Conda documentation
===================

This repository includes documentation for all of conda, including
conda-build.

Feel free to make pull requests against this repo for suggested changes. All
changes are welcome, from typo fixes to new documents to refactoring.

This document will help you get up and running with editing, building, and viewing the documentation from the source tree.

There are two pieces in this repository: the conda landing website at http://conda.pydata.org/ and the actual docs are at http://conda.pydata.org/docs/.

Website
=======

If you do not have conda installed yet, you can do so from http://conda.pydata.org/miniconda.html.

Create and activate a conda environment with the dependencies for building the website

    conda create --name conda-docs --channel asmeurer sphinxjp.themes.basicstrap cloud_sptheme
    activate conda-docs

Use

    cd conda-docs/web
    make html

to build the site.  The result will be in web/build/html.

To check that the links are correct, use

    make linkcheck

Docs
====

If you wish to work on the actual documentation, you must also install conda-docs-deps and conda-build

    activate conda-docs
    conda install --channel asmeurer conda-docs-deps

Furthermore you will need to have conda-build installed in the root environment to generate the help
pages for the conda-build commands.

    conda install --name root conda-build

Unfortunately the conda-docs-deps package is not available for Windows because
we do not have a conda package for perl on Windows yet.

Then run

    cd docs
    make html

The result will be in docs/build/html.

Deploying
=========

The website and docs are deployed automatically to GitHub pages (the
`gh-pages` branch on this repo) with Travis CI when commits are pushed to
master. Travis will build docs on pull requests to make sure there are no
build warnings or errors, but it only deploys it on master.

The site http://conda.pydata.org points to the GitHub pages of this repo.
