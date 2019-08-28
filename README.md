# Nextstrain environment for Conda

[Conda](https://conda.io) is a package and environment manager for Windows, macOS, and Linux that can help ease software installation and usage.

The `nextstrain.yml` file in this repo is hosted at <http://data.nextstrain.org/nextstrain.yml> and serves as an environment definition for Conda.

You can set it up by running:

    curl http://data.nextstrain.org/nextstrain.yml -o nextstrain.yml
    conda env create -f nextstrain.yml
    conda activate nextstrain
    npm install --global auspice

For more details, refer to our [local installation](https://nextstrain.org/docs/getting-started/local-installation/) documentation.
