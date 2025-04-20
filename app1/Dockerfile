# Reference: https://stackoverflow.com/questions/48561981/activate-python-virtualenv-in-dockerfile

FROM python:3.12 AS compiler

ENV PYTHONUNBUFFERED=1
ENV PATH="/opt/venv/bin:$PATH"
ENV POETRY_VIRTUALENVS_IN_PROJECT="false"
ENV POETRY_VIRTUALENVS_PATH="/opt/venv/bin"

WORKDIR /app1/

RUN python -m venv /opt/venv
COPY ./requirements.txt /app1/requirements.txt
COPY ./pyproject.toml /app1/pyproject.toml

RUN pip install -r requirements.txt
RUN poetry install --no-root

COPY . /app1/

EXPOSE ${FASTAPI_PORT}

CMD ["sh", "-c", "poetry run uvicorn app.main:app --host 0.0.0.0 --port ${FASTAPI_PORT}"]
