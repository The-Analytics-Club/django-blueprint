# Blueprint: A Perfect Python Project Structure

Blueprint is an exampel python project you can use to build maintainable applications. The details on the best practices followed in this project are explained in [The Analytics Club](https://www.the-analytics.club)

<a href='https://ko-fi.com/analyticsclub' target='_blank'><img height='35' style='border:0px;height:46px;' src='https://az743702.vo.msecnd.net/cdn/kofi3.png?v=0' border='0' alt='Buy Me a Coffee at ko-fi.com' />

## Installation

Blueprint uses Poetry for dependency management. If you haven't installed it already please use Poetry's [official docs](https://python-poetry.org/docs/#installation) for instructions.

1. Fork this repository by clicking on the fork button at the top right corner. (If not make sure you change the remote url once you cloned this repository)
2. Clone your new repository to your local computer

```bash
git clone git@github.com:thuwarakeshm/blueprint.git
cd blueprint
```

3.Install project depenencies.

```bash
poetry install
```

4. Install pre-commit hooks

```bash
poetry run pre-commit install
```

You are ready to rock.

## Usage

You can activate the Poetry virtualenv with the follwing command:

```bash
poetry shell
```

All the django management commands shall work from now.

```bash
python manage.py runserver
python manage.py makemigrations
python manage.py migrate
python manage.py collectstatic
...
```

**To change the main module name**, you can rename the `blueprint` directory. But make sure you also rename the `name` in the `pyproject.toml` file.

Django apps usually store configuration values in the settings.py itself. But in certain cases, you may want to maintain is seperately. For instance, if you are running django along with celery, celery don't have access to settings.py.

Hence, you can add your config values to the TOML file directly under the `app` section and access it anywhere in your app. The following lines will do the trick.

```python
import toml
APPCONFIG=toml.load('pyproject.toml')['app']
```

Also you can add app secrets directly to the `.env` file and read it anywhere from your project with the help of Python's built in `os` module.

```python
import os
secret = os.getenv('APP_SECRET')
```

This is possible even on development server because we've loaded the env file in our `manage.py` module.
