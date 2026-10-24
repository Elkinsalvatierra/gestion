# DjangoAuth-CRUD

![Home](https://github.com/JFOZ1010/DjangoAuth-CRUD/blob/main/home.png)

This is a simple Django project that implements a CRUD (Create, Read, Update, Delete) application with user authentication.

## Installation

1. Clone the repository.
    
    ```bash
    git clone https://github.com/JFOZ1010/DjangoAuth-CRUD/
    ```

2. Create a virtual environment and activate environment.
        
    ```bash
    python3 -m venv venv
    ```
    
    ```sh
    MacOs/Linux: ./venv/bin/activate
    Windows: .\venv\bin\activate
    ```

3. Install the requirements.

    ```sh
    pip install -r requirements.txt
    ```

4. Run the server.

    ```bash
    python manage.py runserver
    ```

## Docker Compose

Build and start Django with PostgreSQL from the project root:

```bash
docker compose up --build
```

The application is then available at `http://localhost:8000`. The entrypoint applies database migrations before starting Django. Stop the services with `Ctrl+C` and remove them with `docker compose down`. To also delete the local PostgreSQL data volume, use `docker compose down -v`.

## CI and simulated deployment

The `CI and simulated deployment` workflow (`.github/workflows/ci.yml`) runs Django tests against PostgreSQL on pushes to `main` or `ci-setup`, pull requests to `main`, and manual dispatches from the Actions tab. After tests pass, it builds the Docker image and uploads it as the `djangoauth-crud-image` artifact for 30 days; no DockerHub account is required.

To run the artifact without Compose, download `djangoauth-crud-image` from the completed workflow run, extract `djangoauth-crud.tar`, then load it:

```bash
docker load --input djangoauth-crud.tar
```

The image needs a PostgreSQL database. The simplest local simulated deployment is to run the checked-out project with Docker Compose:

```bash
docker compose up --build
```

See [deploy-notes.md](./deploy-notes.md) for the workflow diagram, deployment steps, and evidence checklist.
