# Nextstrain environment for Conda

[Conda](https://conda.io) is a package and environment manager for Windows, macOS, and Linux that can help ease software installation and usage.

The `nextstrain.yml` file in this repo is hosted at <http://data.nextstrain.org/nextstrain.yml> and serves as an environment definition for Conda.

We strongly recommend [Mamba](https://github.com/mamba-org/mamba) as a faster, drop-in replacement for the default Conda installer.

    conda install -c conda-forge mamba

After installing Mamba, setup the Nextstrain environment by running:

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
