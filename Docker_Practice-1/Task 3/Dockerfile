# Stage 1 — install dependencies into isolated directory
FROM python:3.12 AS deps

WORKDIR /build
COPY requirements.txt .
RUN pip install --target=/deps -r requirements.txt

# Stage 2 — runtime
FROM python:3.12 as final

WORKDIR /app
COPY --from=deps /deps /deps
COPY main.py .
ENV PYTHONPATH=/deps

ENTRYPOINT [ "python", "main.py" ]