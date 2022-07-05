# TL;DR

This is a basic setup to run a Jupyter Notebooks (JN) in a a VSCode `devcontainer`. It'll run both the [Miniconda](https://docs.conda.io/en/latest/miniconda.html) run-time environment as well as a PostgreSQL database container. 

# How to Use

If you (re)build the container you can pass environment variables via a `environment.yml*` file located in the project root. See the [Dockerfile](./devcontainer/Dockerfile) for more information.

The python module to allow for a `.env` file is included in the [requirements](./requirements.txt) file. Either create a `.env` file or rename the `env.sample` file and add environment variables in the standard format:

```console
MY_ENV_VAR=some-cool-value
```

As per usuall, add any additional python modules you need to the [requirements](./requirements.txt) file and rebuild the container to have the changes applied.

Finally, when rebuilding the container the [Dockerfile](./devcontainer/Dockerfile) will expect to find a `tar.gz` file with the [OpenShift CLI](https://docs.openshift.com/container-platform/4.9/cli_reference/openshift_cli/getting-started-cli.html) in it. You can get this from afore mentiond link. I use include it because quite allot of my work relates to [MLOps](https://en.wikipedia.org/wiki/MLOps) for which we use OpenShift.

# LICENSE

The [Miniconda](https://docs.conda.io/en/latest/miniconda.html), a minimial distribution of [Anaconda](https://www.anaconda.com/], base image has licencing requirements outside of the free tier for Students, academics, and hobbyists. You may be covered if run within GitHub CodeSpaces but do your due-diligance with respect to licencing.
