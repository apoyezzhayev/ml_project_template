# Production

This is the space for production code: tested Python libs, jobs, services and tools

## Structure

- **[jobs](./training-job/)** (Python/Docker): Combines required data exports, preprocessing and training scripts into a Docker container. This makes results reproducible and the production model retrainable in _any_ ennvironment.
  - **[evaluation](./jobs/evaluation/)**: jobs for evaluation of models from model registry
  - **[inference](./jobs/inference/)**: jobs for batch inference, e.g. the whole dataset or big batch of data
  - **[processing](./jobs/processing/)**: jobs for other processing tasks, not using NN based approaches 
  - **[training](./jobs/training/)**: jobs for training of the model
  - **[job pipelines](./jobs/pipelines/)**: pipelines of the defined jobs
- **[services](./inference-service/)** (Python/Docker): Docker container that provides the final model prediction capabilities via a REST API.
- **[tests](./production/tests/)** (Python): tests for utils library
- **[tools](./production/tools/)** (Python/Bash): any scripts usde for defined preprocessings, model launches, etc. 
- **[src](./production/src/)** (Python): Production code and utility functions that are distilled from the research phase and used across multiple scripts. Should only contain refactored and tested Python scripts/modules. Installable via pip.

## Installation

### Build package

Steps for installation and requirements:

1) Git clone
2) Install system packages: `install.sh`
3) Optionally install python-packages: `requirements.txt` | `conda_env.yaml`
4) Set-up necessary env variables
5) Other set-up steps
6) `pip install -e .`

### Docker Build

Execute this command in the project root folder to build this project and the respective docker container:

```bash
python build.py
```

This script compiles the project, assembles the various artifacts (executable service, client, sources) and builds a docker container with the assembled executables.

 For additional script options:

```bash
python build.py --help
```

## Deploy

Execute this command in the project root folder to deploy all assembled artifacts to our repository and push all docker images to the configured docker registry:

Describe here build and run arguments and corresponding config files

```bash
python build.py --deploy --version={MAJOR.MINOR.PATCH-TAG}
```

For deployment, the version has to be provided. The version format should follow the [Semantic Versioning](https://semver.org/) standard (MAJOR.MINOR.PATCH). For additional script options:

```bash
python build.py --help
```

### Configure Docker Repository

```bash
docker login docker-repository
```

## Dev Guidelines

### Code Style

Our coding guideline for source code are described [here](https://youtrack.netvision-internal.ru/articles/DSD-A-60/TODO:-Code-style)

### Git Workflow

Our git branching for all repositories is based on [these](https://youtrack.netvision-internal.ru/articles/DSD-A-44/Development-common-practices) guidelines.

#### Build Versioning

Our build versioning for all projects is based on the [Semantic Versioning specification](https://semver.org/). For any versioning-related questions, please refer to the [linked guide](https://semver.org/). In additon to the MAJOR.MINOR.PATCH format, a `SNAPSHOT` tag will be attached to the version for all development builds (based on the [Maven versioning standard](https://docs.oracle.com/middleware/1212/core/MAVEN/maven_version.htm)). As define in  Git-Flow, the build version is also used as tag for releases on the master branch.
