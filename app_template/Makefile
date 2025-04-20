# Variables
VENV_DIR = .venv
PYTHON = python3
PIP = $(VENV_DIR)/bin/pip3
POETRY = $(VENV_DIR)/bin/poetry
ACTIVATE = source $(VENV_DIR)/bin/activate
APP_NAME = app_name
REGISTRY = fllsouto.proj
IMAGE_NAME = image_name
IMAGE_TAG = v1.0.0
IMAGE_TAG_NAME = $(REGISTRY)/$(IMAGE_NAME):$(IMAGE_TAG)
ENV_FILENAME = .env

FASTAPI_PORT ?= 8000
HOST ?= 0.0.0.0
HOST_PORT = $(FASTAPI_PORT)
CONTAINER_PORT = $(FASTAPI_PORT)


# Create a virtual environment in project root
venv:
        $(PYTHON) -m venv $(VENV_DIR) && \
        $(PIP) install --upgrade pip && \
        $(PIP) install -r requirements.txt

# Install dependencies using Poetry
install:
        $(POETRY) install --no-root

# Run FastAPI application
run:
        $(POETRY) run uvicorn src.main:app --host $(HOST) --port $(PORT) --reload

# Run Tests
test-unit:
        $(POETRY) run pytest -v -s -m unit tests/

# Clean up the virtual environment
clean:
        rm -rf $(VENV_DIR)

# Docker Commands
docker-build:
        docker build --no-cache -t $(IMAGE_TAG_NAME) .

docker-quick-build:
        docker build -t $(IMAGE_TAG_NAME) .

docker-run:
        docker run --rm -d -p $(HOST_PORT):$(CONTAINER_PORT) --env-file $(ENV_FILENAME) $(IMAGE_TAG_NAME)

docker-compose-up:
        docker compose up --build

docker-compose-down:
        docker compose down

docker-build-and-run: docker-quick-build
        docker compose up
