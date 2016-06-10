# Shamrok

## Getting the environment ready

1. Clone the repository. `git clone https://github.com/PaulOlteanu/Shamrock.git`

2. Get the virtualenv set up. This avoids having to install the libraries globally. This command will also install the required dependencies `make venv`

3. Test it. These should all pass. `make test`

4. Create the database. This should be a postgresql database, with no password with the name of "Shamrock". After installing postgres: `createdb Shamrock`

5. Apply the schema to the database. `./manage.py db upgrade`

## Running the server

1. Run the server. `./manage.py runserver`

The server will run in debug mode by default. Current there is not a way to run in prod mode.

## Description of all routes

| Request Type | Route | Description |
|:---:|:---:|:---:|
| GET | / | API welcome |
| GET | /images | List of all images in the order they were created, in pages of 20 images. Argument `page` specifies which page, or defaults to 1 |
| POST | /images | Upload an image. Data must be form-encoded, with `file` as the name for the file upload, and `title` as the name for the title to save with the image |
| GET | /images/new | List of images, from newest to oldest, in pages of 20 images. Argument page specifies which page, or defaults to 1 |
| GET | /images/hot | List of all images sorted using a special algorithm based on age and number of upvotes, in pages of 20 images. Argument page specifies which page, or defaults to 1 |
| POST | /images/upvote/<id> | Upvotes the image with the specified `id` |

## Directory structure

* /app/: Code for the server itself
    * \__init__.py: Called when importing `app`. Also declares the app folder a package
    * app.py: Code for the server. Returns a flask app object
    * libs.py: Code not coupled to flask
    * models.py: Code containing the model definitions for the database
    * settings.py: The config settings for various environments


* /migrations/: Autogenerated migrations for the database


* /tests/: Various tests for the app
    * conftest.py: Code for creating the test client
    * test_libs: Tests for lib functions
    * test_models: Tests for database functions
    * test_urls: Tests for app routes using HTTP requests


* Makefile: Helpers for creating a venv, installing dependencies, and testing

* manage.py: Runner for the server, and functions for creating the database, creating migrations, and running migrations

* requirements.txt: All the prerequisites for running the application
