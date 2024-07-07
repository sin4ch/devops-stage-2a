# Use the official Python image from the Docker Hub
FROM python:3.11-slim

# Set the working directory inside the container
WORKDIR /app

# Install system dependencies for PostgreSQL
RUN apt-get update && apt-get install -y \
    postgresql-client

# Install Poetry - Python dependency management tool
RUN pip install poetry

# Copy the pyproject.toml and poetry.lock files
COPY pyproject.toml poetry.lock ./

# Install Python dependencies using Poetry
RUN poetry install --no-root

# Copy the rest of the backend application code to the working directory
COPY . .

# Set environment variables required by the application
ENV DOMAIN=localhost \
    ENVIRONMENT=local \
    BACKEND_CORS_ORIGINS=http://localhost,http://localhost:5173,https://localhost,https://localhost:5173 \
    SECRET_KEY=changethis123 \
    FIRST_SUPERUSER=devops@hng.tech \
    FIRST_SUPERUSER_PASSWORD=devops#HNG11 \
    USERS_OPEN_REGISTRATION=True \
    EMAILS_FROM_EMAIL=info@example.com \
    SMTP_PORT=587 \
    POSTGRES_SERVER=localhost \
    POSTGRES_PORT=5432 \
    POSTGRES_DB=app \
    POSTGRES_USER=app \
    POSTGRES_PASSWORD=changethis123

# Expose port 8000 for the FastAPI application
EXPOSE 8000

# Command to run the FastAPI server using Uvicorn
CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
