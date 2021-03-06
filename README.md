# Emoj

[![CircleCI](https://circleci.com/gh/miroesli/emoj.svg?style=shield)](https://circleci.com/gh/miroesli/emoj)

A virtual board game engine for the Seng 499 design project course by **E**mily, **M**isha, **O**leg, and **J**uan.

## Requirements

- [Python 3.8](https://www.python.org/downloads/)
- [Postgres 12](https://www.postgresql.org/download/)
- [psycopg](https://www.psycopg.org/docs/install.html)
- [Virtualenv (optional)](https://virtualenv.pypa.io/en/stable/installation.html)

## Presentation

Project #37 in the [Virtual Open House of UVic 499 Course Projects](https://www.ece.uvic.ca/~fayez/courses/499/index.html)
- [Poster Link](https://www.ece.uvic.ca/~fayez/courses/499/posters/37.pdf)
- [Video Link](https://admin.video.ubc.ca/html5/html5lib/v2.82.2/mwEmbedFrame.php/p/180/uiconf_id/23451293/entry_id/0_9haqlmuh?wid=_180&iframeembed=true&playerId=kaltura_player&entry_id=0_9haqlmuh&flashvars[streamerType]=auto&flashvars[localizationCode]=en&flashvars[leadWithHTML5]=true&flashvars[sideBarContainer.plugin]=true&flashvars[sideBarContainer.position]=left&flashvars[sideBarContainer.clickToClose]=true&flashvars[chapters.plugin]=true&flashvars[chapters.layout]=vertical&flashvars[chapters.thumbnailRotator]=false&flashvars[streamSelector.plugin]=true&flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&flashvars[dualScreen.plugin]=true&flashvars[hotspots.plugin]=1&flashvars[Kaltura.addCrossoriginToIframe]=true&&wid=0_0xk6xbpz)

## Running locally

### Step 1: Clone or fork the repository and change current directory

```bash
git clone https://github.com/emilysluis/emoj.git
cd emoj
```

### Step 2: Install python3 and header files

```bash
sudo apt install python3 python3-dev
```

<!-- libpq-dev? -->

### Step 3: Install postgres 12

```bash
sudo apt install postgresql postgresql-contrib
```

### Step 4: Get python packages

```bash
python -m pip install -r requirements.txt
```

#### Consider using virtualenv (Optional)

Install virtualenv

```bash
pip3 install virtualenv
```

Create an env directory for python3

```bash
virtualenv -p python3 env
```

Enable the virtualenv

**On Linux**

```bash
source env/bin/activate
```

**On Windows**

```bash
env\Scripts\activate.bat
```

Use `deactivate` to stop exit the environment

### Step 5: Create the database

```bash
sudo -u postgres psql -f project/sql/init.sql
psql -U toggleme -d project -f project/sql/create.sql
psql -U toggleme -d project -f project/sql/test_data.sql
```

### Step 6: Run the server

```bash
python manage.py makemigrations && python manage.py migrate
python3 project/manage.py runserver 8000
```

### Step 7: View Application

Access the server in browser at `http://localhost:8000`

## Create User

Run createsuperuser with manage.py

```bash
python manage.py createsuperuser
```

## Runnning in Docker

### Requirements

- [docker](https://docs.docker.com/engine/install/)
- [docker-compose](https://docs.docker.com/compose/install/)

### Execution

Build and run server. `-d` puts it into the background.

<!-- sudo docker build --tag emoj:1.0 . -->

```bash
docker-compose up [-d] --build --remove-orphans
```

Migrating data in another terminal

```bash
sudo docker-compose exec web python project/generate_cards.py
sudo docker-compose exec web python manage.py migrate --no-input
```

To connect to docker database

```bash
docker-compose exec db psql -U postgres -d task_management
```

To remove mapping

```bash
docker-compose down --volumes
docker-compose rm db
```

## Testing

Change directory to the project module

```bash
cd emoj/project
```

Run the test using `manage.py`

```bash
python manage.py test
```

Alternatively to specify which test files

```bash
python manage.py test --pattern="tests_*.py"
```

### Circleci

To test circleci script see the circleci local [installation docs](https://circleci.com/docs/2.0/local-cli/#installation)

## :heart: Credits & Thanks

- Dr Miguel Nacenta for guiding us in our design decisions.

