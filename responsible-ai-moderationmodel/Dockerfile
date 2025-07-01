# Use Python 3.9 base image for amd64 architecture
FROM --platform=linux/amd64 python:3.9-slim

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive \
    PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    HF_HOME=/app/huggingface_cache \
    LOG_DIR=/app/logs

# Set working directory
WORKDIR /app

# Copy app files
COPY . .

# Copy models folder explicitly -please work this time
COPY models /app/models

# EXPLICTLY PUTTING PERMISSIONS TO MODELS FOLDER
RUN chmod -R 755 /app/models

# Upgrade pip
RUN python -m pip install --upgrade pip

# Install dependencies (change the torch url to something that uses CUDA for GPU support)
RUN pip install -r requirements/requirement.txt \
    && pip install werkzeug \
    && pip install torch==2.2.0 --index-url https://download.pytorch.org/whl/cpu

# Expose Flask port
EXPOSE 8000

# Run the Flask app
CMD ["python", "src/main.py"]
