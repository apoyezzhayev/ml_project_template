# Research 

Scripts and Notebooks for experimentation.


> #TODel Describe in `Structure` chapter the structure of research subfolders and notebooks.
> Add here only top-level descriptions:
> -  For single notebooks experiments add here description of the notebook and a reference to it
> -  For subfolder experiments (if supplementary files are required) add here description of the experiment and name of the main notebook

## Structure

- **[develop](./develop)** (Python/Notebooks): Experimental code to try out new ideas and experiments. Use Jupiter notebooks wherever you can. Naming convention: `{US_id}{task_id}_{YYYY-MM-DD}_{user_id}_{short-description}`. If you cannot use a single notebook and have multiple scripts/files for an experiment, create a folder with the same naming convention. Each file should be handled by one person only.
- **[deliver](./deliver)** (Python/Notebooks): Refactored notebooks that contain valuable insights or results (e.g. visualizations, training runs). Notebooks should be refactored, documented, contain outputs, and use the following naming schema: `{US_id}_{date}_{short-description}`. Notebooks in deliver should not be changed or rerun. If you want to rerun a deliver Notebook, please duplicate it into the develop folder.
   - **[runs](./deliver/runs)** (Python/Notebooks): Runs and visualizations of training/validation/inference tasks, if it was launched inside notebook (not as separate job)
   - other types of tasks may be placed into the root of the directory
- **[templates](./templates)** (Python/Notebooks): Refactored Notebooks that are reusable for a specific task (e.g. model training, data exploration). Notebooks should be refactored, documented, not contain any output, and use the following naming schema: `short-description`. If you like to make use of a template Notebook, duplicate the notebook into develop folder.

## Policies

- Use naming conventions for notebook and subfolders
- If an experiment requires supplementary files for notebook, create subfolder with naming convention as for notebooks and add there all necessary files
- Don't upload data files (images, annotations, checkpoints etc.) to the repository. Instead, use the download script or cell in notebook for downloading necessary data for an experiment inside `.../exp_id/tmp` 
- Don't use absolute paths inside your notebook like `/home/user/data/...`, instead use relative paths like `./tmp/data`
- Structure your notebooks with headings of different levels
- Provide `requirements.txt` or devote first chapter of the notebook to installation of requirements in cells
- If you need to save some information or outputs use `./tmp/logs|results|etc` folder for it
- Use plugins for your IDE for convenient notebooks difference viewing that doesn't include meta information
- Try not to upload `deliver` notebooks with long log outputs, instead use external logging or hide the cell
- Try to distill reusable functions and classes into `utils.py` or a set of modules which are imported in the first cell of the notebook
- Try not to use `sys.path.append` imports, use temporary installations instead (`pip install -e .`)
