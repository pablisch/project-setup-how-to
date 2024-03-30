# Setting up a Python project with Pytest

```bash
# ensure that the pip package manager is installed and up to date for the specified Python interpreter
python3 -m ensurepip --upgrade

# check your python version
python3 --version

# Add the pytest package to your project
pipenv install pytest

# Add directorys and files
mkdir tests lib
touch tests/__init__.py lib/__init__.py

# Run our tests
pytest -x

# Initialize a git repository and make an initial commit
git init
git add .
git commit -m "Project setup with Pytest."
```

## Create your virtual environment

```bash
# Create a virtual environment using venv
python3 -m venv <name_of_virtual_environment_venv>

# Activate the virtual environment
source <name_of_virtual_environment_venv>/bin/activate
```

## Deactivate your virtual environment

```bash
# Deactivate the virtual environment
deactivate
```

