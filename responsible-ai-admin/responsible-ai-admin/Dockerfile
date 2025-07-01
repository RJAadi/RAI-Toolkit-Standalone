# Use platform-specific base image for EKS (amd64)
FROM --platform=linux/amd64 python:3.9-slim

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Create a non-root user
RUN adduser --disabled-password --gecos '' myuser

# Set work directory
WORKDIR /app

# Copy only requirements first for better cache
COPY requirement/requirement.txt ./requirement.txt

# Install system dependencies and Python requirements
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender-dev \
    tesseract-ocr \
    poppler-utils \
    && pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirement.txt \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Copy entire source code to working directory
COPY . .

# Switch to non-root user
USER myuser

# Expose port (adjust if different in main.py)
EXPOSE 8000

# Set working directory for entrypoint
WORKDIR /app/src

# Entrypoint command
CMD ["python", "main.py"]
