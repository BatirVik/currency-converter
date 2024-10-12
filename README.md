# Currency Converter
The backend API service for storing and managing currencies, along with a simple one-page frontend that fetches available currencies and implements conversion logic.

## Quick Start
```bash
MOCK_CURRENCIES=true docker-compose up --build
```
API docs: http://localhost:8000/docs \
Frontend: http://localhost:8000

## Backend

### Environment variables

**ENV**
> Based on this value, the configuration will load a specific .env file from the configuration folder.\
Available values: **production** (.env), **development** (.env.dev), **test** (.env.test)

**DB_URL**
> URL of the database

**LOGS_PATH**
> Path to the file for writing logs

**SECRET_KEY**
> The minimum length is 32 characters, generate with `openssl rand --hex 32`.

**ALGORITHM** / optional
> JWT algorithm, by default "HS256"

**ACCESS_TOKEN_EXPIRE_MINUTES** / optional
> JWT token lifetime, by default "15"

### Testing
Run a postgresql docker:
```bash
docker run -d -p 5100:5432 -e POSTGRES_DB=test -e POSTGRES_USER=test -e POSTGRES_PASSWORD=test postgres
```
Create the configuration/**.env.test** file:
```env
DB_URL="postgresql+psycopg://test:test@localhost:5100/test"
SECRET_KEY= # openssl rand --hex 32
LOGS_PATH="logs/logs.test.txt"
```
Run pytest: (ENV will be overridden to 'test' even if it was exported with a different value)
```bash
poetry run pytest
```

### Migrations
Activate the virtual environment and define ENV:
```bash
poetry shell
export ENV=development
```
Create migration file:
```bash
alembic revision --autogenerate -m "message"
```
Apply latest migrations:
```bash
alembic upgrade head
```

### Scripts
Activate the virtual environment and define ENV:
```bash
poetry shell
export ENV=development
```
#### Create user
```bash
python manage.py create-user "email" "password"
```
#### Create admin
```bash
python manage.py create-admin "email" "password"
```
#### Load mock currencies
```bash
python manage.py create-mock-currs
```

