# Stage 1 — install dependencies into isolated directory
FROM python:3.12 AS deps
EXPOSE 8080

WORKDIR /build
COPY requirements.txt .
RUN pip install --target=/deps -r requirements.txt


# Stage 2 — build / compile step (placeholder, e.g. for Cython)
FROM python:3.12 AS builder

RUN apt-get update && apt-get install -y libpq-dev
COPY --from=deps /deps /deps
ENV PYTHONPATH=/deps
COPY . /build
WORKDIR /build
RUN python -m build


# Stage 3 — runtime
FROM python:3.12 as final

WORKDIR /app

COPY --from=builder /deps /deps
ENV PYTHONPATH=/deps

COPY . /app


ENTRYPOINT [ "python", "main.py" ]