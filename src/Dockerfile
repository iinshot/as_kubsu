FROM python:3.10-slim AS builder
WORKDIR /app
COPY pyproject.toml .
RUN mkdir -p src && touch src/__init__.py
RUN pip install --no-cache-dir --user ".[test]"

FROM python:3.10-slim
WORKDIR /app
COPY --from=builder /root/.local /root/.local
COPY src/ ./src/
COPY tests/ ./tests/
ENV PATH=/root/.local/bin:$PATH
ENTRYPOINT ["uvicorn"]
CMD ["src.main:app", "--host", "0.0.0.0", "--port", "8006"]