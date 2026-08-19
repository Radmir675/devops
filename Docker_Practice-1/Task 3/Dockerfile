# Stage 1 — install dependencies into isolated directory
FROM python:3.12 AS deps
EXPOSE 8080

WORKDIR /build
COPY requirements.txt .
RUN pip install --target=/deps -r requirements.txt


# Stage 2 — build / compile step (placeholder, e.g. for Cython)
FROM python:3.12 AS builder

COPY --from=deps /deps /deps
ENV PYTHONPATH=/deps
COPY . /build
WORKDIR /build


# Stage 3 — runtime
FROM python:3.12

RUN apt-get update && apt-get install -y libpq-dev

WORKDIR /app

COPY --from=deps /deps /deps
ENV PYTHONPATH=/deps

COPY . /app


ENTRYPOINT [ "python", "main.py" ]