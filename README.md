# ML Project Template

#TODel: This repository contains a template project that can be easily adapted for all kinds of Machine Learning tasks. 
Typically, solving such task entails two main phases, _research_ and _production_ with very different focuses. The template intends to facilitate work on ML projects by guiding practitioners to adopt some best practices. It is recommended to simply clone this repo and customize it to the specific use-case at hand.

***

## Project description

#TODO:
- Overview
- Goal
- Problems

## TOC

Table of contents

***

## Useful resources

#TODO:
- Wiki article of the project in knowledge base
- S3 bucket of the project
- Experiment manager project
- NFS/Google disk, etc.
- Diagrams folder of the project
- Other docs

***

## [Features]

#TODO: Optional features description

## Installation guide

### From source

#TODO: Step-by-step installation guide

### [Docker]

#TODO: If docker image is present or Docker file, the main arguments description

## Building the documentation

#TODO: Describe here the documentation building process and reference to documentation

***

## Getting started

#TODO: getting started demo notebooks of core functionality with direct links

***
## License

#TODO: license

***

## Structure

[`research`](./research): EDA, model prototyping
and training experiments are dumped here in a structured way.

[`production`](./production): distilled utils lib, training job and inference service are implemented here.

***

## Repository Structure
### Static
- **[assets](./assets)**: any assets that are used for `README.md` files and other
- **[LICENSE](./LICENSE)**: license information
- **[README.md](./README.md)**: top-level readme file with description of the repository and project

### Dynamic
- **[configs](./configs)** (Python/YAML/JSON): configuration files for any type of tasks, scripts, models and data-pipelines initialization
- **[data](./data)**: directory containing data for training and evaluation, data transformation scripts and notebooks. Most files and child directories from this folder will not be pushed to the repo's remote, it is declared only for convenience and preservation of the repository's structure. Use the naming convention for persistent and temporary datasets: `{ds_name}_{state}_{additional_desc}_{version}`
    - **[raw](./data/raw)**: folder for raw files temporary storage. Use it for downloading external datasets. Datasets in the directory must be non-mutable. `non pushable`
    - **[processed](./data/processed)**: folder for local storage of processed datasets. `non pushable`
    - **[tmp](./data/tmp)**: folder for storing temporary files and intermediate data processing results. Moreover, this folder is used for storing caches of our streamable datasets from the data registry. `non pushable`
    - **[scripts](./data/scripts)** (Python/Notebooks): scripts for downloading/uploading data to registry and transformations.
    - **[eda](./data/eda)** (Notebooks): Exploratory Data Analysis of input datasets. Every EDA notebook must be duplicated to the data registry `dareg`. Notebooks must be documented, structured, contain cell outputs.
- **[research](./research)**: Scripts and Notebooks for experimentation.
  - **[develop](./research/develop)** (Python/Notebooks): Experimental code to try out new ideas and experiments. Use Jupyter notebooks wherever you can. Naming convention: `{US_id}{task_id}_{YYYY-MM-DD}_{user_id}_{short-description}`. If you cannot use a single notebook and have multiple scripts/files for an experiment, create a folder with the same naming convention. Each file should be handled by one person only.
  - **[deliver](./research/deliver)** (Python/Notebooks): Refactored notebooks that contain valuable insights or results (e.g. visualizations, training runs). Notebooks should be refactored, documented, contain outputs, and use the following naming schema: `{US_id}_{date}_{short-description}`. Notebooks in deliver should not be changed or rerun. If you want to rerun a deliver Notebook, please duplicate it into the develop folder.
     - **[runs](./research/deliver/runs)** (Python/Notebooks): Runs and visualizations of training/validation/inference tasks, if it was launched inside notebook (not as separate job)
     - other types of tasks may be placed into the root of the directory
  - **[templates](./research/templates)** (Python/Notebooks): Refactored Notebooks that are reusable for a specific task (e.g. model training, data exploration). Notebooks should be refactored, documented, not contain any output, and use the following naming schema: `short-description`. If you like to make use of a template Notebook, duplicate the notebook into develop folder.
  
- **[production](./production)**: The production-ready solution(s) composed of libraries, services, and jobs.
  - **[jobs](./production/training-job/)** (Python/Docker): Combines required data exports, preprocessing and training scripts into a Docker container. This makes results reproducible and the production model retrainable in _any_ environment.
    - **[evaluation](./production/jobs/evaluation/)**: jobs for evaluation of models from model registry
    - **[inference](./production/jobs/inference/)**: jobs for batch inference, e.g. the whole dataset or big batch of data
    - **[processing](./production/jobs/processing/)**: jobs for other processing tasks, not using NN based approaches 
    - **[training](./production/jobs/training/)**: jobs for training of the model
    - **[job pipelines](./production/jobs/pipelines/)**: pipelines of the defined jobs
  - **[services](./production/inference-service/)** (Python/Docker): Docker container that provides the final model prediction capabilities via a REST API.
  - **[tests](./production/tests/)** (Python): tests for utils library
  - **[tools](./production/tools/)** (Python/Bash): any scripts used for defined preprocessings, model launches, etc. 
  - **[src](./production/src/)** (Python): Production code and utility functions that are distilled from the research phase and used across multiple scripts. Should only contain refactored and tested Python scripts/modules. Installable via pip.

## Template usage

- Add LICENSE
- Rename `production/src` to your project's name if necessary
- Delete corresponding `.gitkeep` files when commit into the directory.
- Delete `TODel` sections in README
- Fill `TODO` sections

### Code Artifacts

- develop notebooks/scripts: `YYYY-MM-DD_userid_short-description`
- deliver notebooks/scripts: `YYYY-MM-DD_short-description`
- template notebooks/scripts: `short-description`
- services: `-service` suffix
- jobs: `-job` suffix
- libraries: `-lib` suffix