# Shamrok

## Getting the environment ready

1. Clone the repository. `git clone https://github.com/PaulOlteanu/Shamrok.git`

2. Get the virtualenv set up. This avoids having to install the libraries globally. This command will also install the required dependencies `make venv`

3. Test it. These should all pass. `make test`

4. Create the database. This should be a postgresql database, with no password with the name of "Shamrok". After installing postgres: `createdb Shamrok`

5. Apply the schema to the database. `./manage.py db upgrade`

## Running the server

1. Run the server. `./manage.py runserver`

## Description of all routes

| Request Type | Route | Description |
|:---:|:---:|:---:|
| GET | / | Home page |
| GET | /images | Page listing all images in the specified sort order, in pages of 20 images. Argument `page` specifies which page, or defaults to 1. Argument `sort` specifies the sorting technique. "new" for new -> old, "hot" for an algorithm based on votes and age, and a default of old -> new
| GET | /upload | Page to upload an image |
| GET | /api | API welcome |
| GET | /api/images | JSON list of all images in the specified sort order, in pages of 20 images. Argument `page` specifies which page, or defaults to 1. Argument `sort` specifies the sorting technique. "new" for new -> old, "hot" for an algorithm based on votes and age, and a default of old -> new |
| POST | /api/images | Upload an image. Data must be form-encoded, with `file` as the name for the file upload, and `title` as the name for the title to save with the image |
| GET | /api/images/`id` | Get the image with the specified `id` |
| POST | /api/images/upvote/`id` | Upvote the image with the specified `id` |

## Directory structure

* /app/: Code for the server itself
    * static/: CSS and JS files
    * templates/: HTML files
    * \__init__.py: Called when importing `app`. Also declares the app folder a package
    * app.py: Code for the server. Returns a flask app object
    * lib.py: Code for generating filenames, and for functions used in both the API, and the HTML rendering
    * models.py: Code containing the model definitions for the database
    * settings.py: The config settings for various environments


* /migrations/: Autogenerated migrations for the database


* /tests/: Various tests for the app
    * \__init.py__: Declares the tests folder a package
    * conftest.py: Code for creating the test client
    * test_api_urls: Tests for api routes using HTTP requests
    * test_libs: Tests for lib functions
    * test_models: Tests for database functions


* Makefile: Helpers for creating a venv, installing dependencies, and testing

* manage.py: Runner for the server, and functions for creating the database, creating migrations, and running migrations

* Procfile: Config file specifying the run command for Heroku

* requirements.txt: All the prerequisites for running the application

* runtime.txt: Specifies the version of python to use for Heroku
