# PiperCI Flake8 Function
[![Build Status](https://travis-ci.com/AFCYBER-DREAM/piperci-flake8-faas.svg?branch=master)](https://travis-ci.com/AFCYBER-DREAM/piperci-flake8-faas)

### Table of Contents

* [Getting Started](#getting-started)
* [Prerequisites](#prerequisites)
* [Installing](#installing)
* [Inputs and Outputs](#inputs-and-outputs)
* [Running the Tests](#running-the-tests)
* [Contributing](#contributing)
* [Versioning](#versioning)
* [Authors](#authors)
* [License](#license)
* [Acknowledgements](#acknowledgments)


## Getting Started

To deploy this function you must have OpenFaaS installed. To create a development environment see (https://github.com/AFCYBER-DREAM/ansible-collection-pidev)

### Prerequisites

OpenFaaS

### Installing

To install this function on OpenFaaS do the following after authentication:

```
git clone https://github.com/AFCYBER-DREAM/piperci-flake8-faas.git
cd piperci-flake8-faas
faas build
faas deploy
```

To validate that your function installed correctly you can run the following:

```
faas ls
```

## Inputs and Outputs

This function expects the following JSON configuration, which will run flake8 with the
default arguments on all files in the artifact specified by the artifact_uri field.

```json
{
  "run_id": "<run_id>",
  "project": "<project_name>",
  "configs": [
    {"files": "*.py"}
  ],
  "stage": "<stage_name>",
  "artifacts": {
    "<artifact_name>": {
	  "artifact_uri": "<uri_for_artifact>",
	}
}
```

One can optionally include the `exclude` field, which will tell flake8 to exclude a file or directory
(a glob can also be specified). When the exclude field is present then the Flake8 FaaS will parse the
files field and apply the exclusion to that file or glob.

```json
{
  "run_id": "<run_id>",
  "project": "<project_name>",
  "configs": [
    {"files": "*.py"},
	{"files": "charon/model/*", "exclude": "true"}
  ],
  "stage": "<stage_name>",
  "artifacts": {
    "<artifact_name>": {
	  "artifact_uri": "<uri_for_artifact>",
	}
}
```


## Running the tests

```bash
tox -e lint
```

### Test Prerequisites

Tox must be installed and an OpenFaaS environment must be available locally.
You must also deploy the image to OpenFaaS.

There is an simple bash script which can be used to turn a local machine into
an OpenFaaS development environment. This can be found in `tools/scripts/setup-env.sh`.
This is the script that is being used by Travis-CI to deploy the test environment.

We also have an ansible role available to setup the OpenFaaS environment. This
can be found [here](https://github.com/AFCYBER-DREAM/ansible-collection-pidev)

## Contributing

Please read [CONTRIBUTING.md](https://github.com/AFCYBER-DREAM/piperci-picli) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/piperci-flake8-faas/tags).

## Authors

See also the list of [contributors](https://github.com/AFCYBER-DREAM/piperci-flake8-faas/contributors) who participated in this project.

## License

MIT
