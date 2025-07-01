# Use Python 3.9 base image for amd64 architecture
FROM --platform=linux/amd64 python:3.9-slim

ENV DEBIAN_FRONTEND=noninteractive

# Set working directory
WORKDIR /app

# Copy the source code
COPY . .

# Install dependencies
RUN pip3 install --no-cache-dir -r src/requirements/requirement.txt

# Install local .whl package
RUN pip3 install --no-cache-dir src/lib/better_profanity-2.0.0-py3-none-any.whl

RUN pip3 install --no-cache-dir src/lib/aicloudlibs-0.1.0-py3-none-any.whl

RUN pip3 install --no-cache-dir src/lib/en_core_web_lg-3.7.1-py3-none-any.whl

# Fix permissions for non-root runtime user - new addition
RUN chown -R 1000:1000 /app

# Set working directory to src
WORKDIR /app/src

# Run the application
CMD ["python3", "main.py"]
