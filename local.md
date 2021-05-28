# Setting up the server locally

To create a local development setup of the care backend and frontend projects, perform the following steps.

## Care Backend

* Install PostgreSQL on your machine. The instructions for the same can be found at [https://www.postgresql.org/download/](https://www.postgresql.org/download/)
  * Change the authentication method to `md5` instead of `peer`. The instructions for the same can be found in this [StackOverflow Answer](https://stackoverflow.com/a/12670521/4385622)
* Install the GDAL and Geos libraries. \( This is required because Care Uses a PostGis database Connection by default, this is to power location fields which can be later be used for better location-based queries   \) On Debian/Ubuntu systems, run `sudo apt-get install libgdal-dev libgeos-dev python-dev` 
* Clone the project: `$ git clone https://github.com/coronasafe/care`
* `$ cd care`
* Create a virtual environment: `$ virtualenv -p $(which python3) venv`
* `$ source venv/bin/activate`
* `$ pip install -r requirements/local.txt`
* Set the DATABASE\_URL environment variable for your Postgres database. \( By default it expects a database with the name "care", only change this variable if your database is named something else \)
* Run the database migrations: `$ python manage.py migrate`
* Create a superuser: `$ python manage.py createsuperuser`  

  `$ python manage.py runserver`

* The project should be running at [http://localhost:8000](http://localhost:8000) API Specs are available at [http://localhost:8000/redoc](http://localhost:8000/redoc) and [http://localhost:8000/swagger](http://localhost:8000/swagger)

## Care Frontend

* Make sure you have Node v10 or above installed on your machine.
* Clone the project: `$ git clone https://github.com/coronasafe/care_fe`
* `$ cd care_fe`
* `$ git checkout master`
* `$ npm install`
* `$ npm run start`

The project should be running at [http://localhost:4000](http://localhost:4000) In order to connect the backend to the frontend, modify proxy target for `/api` in webpack.config.js

