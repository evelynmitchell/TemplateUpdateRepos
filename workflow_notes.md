This project uses poetry for managing the venv for python.

The poetry.lock file was created with:

```
poetry install
```
and will only need to be done at the beginning of the project, or when the version number of the project is updated (?).

To activate the virtual environment before beginning a programming session, run:

```
poetry shell
```

To use the project within this virtual environment, run:

```
cd src
poetry run python
  >>> import template_repo_update
```
If you try to import template_repo_update from the project directory you will get a ModuleNotFoundError. (There are at least 4 ways to get this error, but making sure you are in the correct directory is the first thing to check.)

To deactivate the virtual environment, run:

```
exit
```
