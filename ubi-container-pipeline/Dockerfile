# Dockerfile

FROM registry.access.redhat.com/ubi9/python-39:latest

LABEL maintainer="Kenneth Barnes Jr" \
      description="Universal Base Image (UBI) Python 3.9 application container"

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

# Switch to root to install packages and create user
USER root

# Create non-root user and app directory
RUN useradd -r -u 1000 ubi_user \
    && mkdir -p /app \
    && chown ubi_user:ubi_user /app

WORKDIR /app

# Copy requirements first so layers cache on deps changes only
COPY requirements.txt /app/requirements.txt

# Install dependencies (use pip from base image)
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY app/ /app

# Change to non-root & has the container listen on port 5000
USER ubi_user

EXPOSE 5000

# Healthcheck to ensure container is responding
HEALTHCHECK --interval=30s --timeout=5s \
CMD python -c "import http.client; conn=http.client.HTTPConnection('localhost', 5000); conn.request('GET', '/'); resp=conn.getresponse(); exit(0 if resp.status == 200 else 1)"

# Starts Flask application
CMD ["python", "ubi_app.py"]
