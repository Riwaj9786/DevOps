version: "3.9"

services:
  web:
    build:
      context: .
      dockerfile: Dockerfile
    volumes:
      - .:/app  # Mount the current directory to /app in the container
      - static_volume:/app/staticfiles  # Persistent storage for static files
      - media_volume:/app/mediafiles    # Persistent storage for media files
    ports:
      - "8000:8000"  # Expose port 8000 for the web application
    env_file:
      - .env  # Load environment variables from a .env file
    depends_on:
      - db  # Wait for the db service to start before starting
    command: python manage.py runserver 0.0.0.0:8000  # Run Django server
    networks:
      - app-network

  db:
    image: postgres:13  # Use PostgreSQL version 13
    volumes:
      - db_data:/var/lib/postgresql/data  # Persist PostgreSQL data
    environment:
      POSTGRES_DB: mydatabase
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
    networks:
      - app-network

  pgadmin:
    image: dpage/pgadmin4  # Use pgAdmin for managing PostgreSQL
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@example.com
      PGADMIN_DEFAULT_PASSWORD: admin
    ports:
      - "5050:80"  # Access pgAdmin at http://localhost:5050
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  static_volume: {}
  media_volume: {}
  db_data: {}
Explanation of Each Section
web Service (Django App)

build: Specifies the Dockerfile to use for building the Django app.
volumes:
Mounts the current directory to /app to allow live code updates during development.
Stores static and media files in persistent Docker volumes.
ports: Maps port 8000 on the container to port 8000 on the host.
env_file: Loads environment variables from a .env file.
depends_on: Ensures db service is started before the web service.
command: Runs the Django development server.
db Service (PostgreSQL)

image: Uses the official PostgreSQL image.
volumes: Stores PostgreSQL data in a persistent volume to retain it between container restarts.
environment: Sets PostgreSQL environment variables for database name, user, and password.
pgadmin Service (Database Management)

image: Uses the official pgAdmin image to manage the PostgreSQL database.
environment: Sets default login credentials.
ports: Exposes pgAdmin on port 5050.
Networks and Volumes

networks: Defines a custom network (app-network) to enable communication between services.
volumes: Persistent volumes for static files, media files, and PostgreSQL data.
Running the Compose File
To start the services, run:

bash
Copy code
docker-compose up -d
This will start all services in detached mode. You can access:

Django app at http://localhost:8000
pgAdmin at http://localhost:5050
