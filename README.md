# Nextstrain environment for Conda

[Conda](https://conda.io) is a package and environment manager for Windows, macOS, and Linux that can help ease software installation and usage.

The `nextstrain.yml` file in this repo is hosted at <http://data.nextstrain.org/nextstrain.yml> and serves as an environment definition for Conda.

Setup the Nextstrain environment by running:

    curl http://data.nextstrain.org/nextstrain.yml -o nextstrain.yml
    conda env create -f nextstrain.yml
    conda activate nextstrain
    npm install --global auspice

For a faster installation process, use [Mamba](https://github.com/mamba-org/mamba) as a drop-in replacement for Conda's installer.

    # Install Mamba
    conda install -c conda-forge mamba

    # Create environment with Mamba.
    curl http://data.nextstrain.org/nextstrain.yml -o nextstrain.yml
    mamba env create -f nextstrain.yml
    conda activate nextstrain
    npm install --global auspice

For more details, refer to our [local installation](https://nextstrain.org/docs/getting-started/local-installation/) documentation.


## Continuous integration and deployment

A [GitHub Actions](https://github.com/features/actions) workflow is [defined in
this repository](.github/workflows/test-and-publish.yml) to test creation of
the Conda environment on Linux (Ubuntu) and macOS every time commits are pushed
or a PR is opened.

If all tests are successful and the push is made to the `master` branch, the
`./publish` script is run to deploy the file to data.nextstrain.org.

AWS credentials are stored in this [repository's
secrets](https://github.com/nextstrain/conda/settings/secrets) and are
associated with the `nextstrain-conda-publisher` IAM user in the Bedford Lab
AWS account, which is locked down to publishing only that file.


## Why does this repo exist?

Historically there were lots of ad-hoc Conda environment files for Nextstrain
(and various subprojects, like Augur).  Some of these still linger because they
were never removed.  They probably should be.

There was also an "official" environment file at
<https://data.nextstrain.org/nextstrain.yml> used in some common installation
instructions.  This file was not in source control and did not have an
authoritative source other than the `nextstrain-data` S3 bucket itself.

In an attempt to address both the proliferation and lack of authoritative
source control for the environment file, I (@tsibley) created this repo in
2019.  It let us start to standardize the Conda environment for Nextstrain.

These days, we no longer refer to <https://data.nextstrain.org/nextstrain.yml>
in [our installation docs](https://docs.nextstrain.org/en/latest/install.html),
because we moved to having official Conda packages instead of an environment
definition. However, it's still referenced widely enough ([for
example](https://github.com/search?q=http%3A%2F%2Fdata.nextstrain.org%2Fnextstrain.yml&type=code))
that I wouldn't want to just remove it unceremoniously.
