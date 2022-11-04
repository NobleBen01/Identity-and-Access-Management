# Coffee Shop Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Environment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virtual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) and [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/) are libraries to handle the lightweight sqlite database. Since we want you to focus on auth, we handle the heavy lift for you in `./src/database/models.py`. We recommend skimming this code first so you know how to interface with the Drink model.

- [jose](https://python-jose.readthedocs.io/en/latest/) JavaScript Object Signing and Encryption for JWTs. Useful for encoding, decoding, and verifying JWTS.

## Running the server

From within the `./src` directory first ensure you are working using your created virtual environment.

Each time you open a new terminal session, run:

```bash
export FLASK_APP=api.py;
```

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

## Tasks

### Setup Auth0

1. Create a new Auth0 Account
2. Select a unique tenant domain
3. Create a new, single page web application
4. Create a new API
   - in API Settings:
     - Enable RBAC
     - Enable Add Permissions in the Access Token
5. Create new API permissions:
   - `get:drinks`
   - `get:drinks-detail`
   - `post:drinks`
   - `patch:drinks`
   - `delete:drinks`
6. Create new roles for:
   - Barista
     - can `get:drinks-detail`
     - can `get:drinks`
   - Manager
     - can perform all actions
7. Test your endpoints with [Postman](https://getpostman.com).
   - Register 2 users - assign the Barista role to one and Manager role to the other.
   - Sign into each account and make note of the JWT.
   - Import the postman collection `./starter_code/backend/udacity-fsnd-udaspicelatte.postman_collection.json`
   - Right-clicking the collection folder for barista and manager, navigate to the authorization tab, and including the JWT in the token field (you should have noted these JWTs).
   - Run the collection and correct any errors.
   - Export the collection overwriting the one we've included so that we have your proper JWTs during review!

### Implement The Server

There are `@TODO` comments throughout the `./backend/src`. We recommend tackling the files in order and from top to bottom:

1. `./src/auth/auth.py`
2. `./src/api.py`



GET https://dev-ki8kr2k0.us.auth0.com/authorize?audience=CoffeeShop&response_type=token&client_id=wbHdLRjFu6dZg80JQyknKsRrRur1rqaX&redirect_uri=https://127.0.0.1:5000/login-results

Manager
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IlJqUjRZZUplN2F5TU45Ri1Zcl81UiJ9.eyJpc3MiOiJodHRwczovL2Rldi1raThrcjJrMC51cy5hdXRoMC5jb20vIiwic3ViIjoiZ29vZ2xlLW9hdXRoMnwxMDgwMzUzNzQwMjIzNzg0ODk0NTUiLCJhdWQiOiJDb2ZmZWVTaG9wIiwiaWF0IjoxNjY2MTc5MzY2LCJleHAiOjE2NjYyNjU3NjYsImF6cCI6IndiSGRMUmpGdTZkWmc4MEpReWtuS3NSclJ1cjFycWFYIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJkZWxldGU6ZHJpbmtzIiwiZ2V0OmRyaW5rcyIsImdldDpkcmlua3MtZGV0YWlsIiwicGF0Y2g6ZHJpbmtzIiwicG9zdDpkcmlua3MiXX0.TjtcmEgoF3jocHv8PJFiOdctB5Sgkxmeh_nRPQXMaMhzMW4WKb7Jfho8dnBSO16ZALJaKRI9jtkvOHbcCmH11ORYugtzIw2gvOaLwqJRUqeNeMJlMVl6O8uiulagsL8GQTxsnKQAnp8JrPU4aj9OwiLEN8W7k_XFPJ5iW67gjInm0EZBBnP2cA9mk1MN9hOAsavvtdWQ5jhVr8RRyT80Yahc_fhrLkb8VWBFYyW8voh9g21lEJmF4Jvlavf10vINHXBsa-Zja9mnHyDMGjWVuKQhQhSRx4_f9sHBzqJdUTOc86HPnYNk1uKkpcy0PycmFgyGT1NshhwuppBQzdpp_w

Barista
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IlJqUjRZZUplN2F5TU45Ri1Zcl81UiJ9.eyJpc3MiOiJodHRwczovL2Rldi1raThrcjJrMC51cy5hdXRoMC5jb20vIiwic3ViIjoiZ29vZ2xlLW9hdXRoMnwxMDI2MzQ0ODI1NDA2ODg1Mzg3MjMiLCJhdWQiOiJDb2ZmZWVTaG9wIiwiaWF0IjoxNjY2MTgyODgxLCJleHAiOjE2NjYyNjkyODEsImF6cCI6IndiSGRMUmpGdTZkWmc4MEpReWtuS3NSclJ1cjFycWFYIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJnZXQ6ZHJpbmtzIiwiZ2V0OmRyaW5rcy1kZXRhaWwiXX0.vvGqY32v4tUoBKNgKIedOIL3kLqRaFwIt45sp5WD0C5FIpW42njMejFxiHceWXbIcdErqEIF-mNTZKG_jBemSr70PiHPr8BU64DaIJHGgcejI2_kXSdbqvi0ZTTKeMc4O8bG-tZpTrkOZPPmfFeo3VIzdx-i9VFCPw7ohT2oYGP1epAz2kmBzu4InyKy-CFY8T-SZQP9fZKe5x53fjmt169t42aUOIqQpq0H6nn3fKqsi5p5-uoZnWoeo0nKG83v8V4EVgrWyEdm8EecTLcfQN94D2uENBgwkGv5uRRgVeN6L-ETY484RH3GVCL1Qq9l_6iWU6seF6JEq9NocFIzpQ