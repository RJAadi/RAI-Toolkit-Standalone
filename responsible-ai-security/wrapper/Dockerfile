# Use Python 3.9 base image for amd64 architecture
FROM --platform=linux/amd64 python:3.9-slim

ENV DEBIAN_FRONTEND=noninteractive
ENV MPLCONFIGDIR=/tmp/matplotlib  
# Matplotlib cache directory to /tmp

# system dependencies
RUN apt-get update && apt-get install -y wkhtmltopdf && apt-get clean

# working directory
#COPY . .
WORKDIR /app
COPY . .
# Copy files
COPY requirements/requirement.txt /app/requirements.txt
COPY lib/adversarial_robustness_toolbox-1.16.0-py3-none-any.whl /tmp/

# COPY app /app  


# Upgrade pip
RUN pip install --upgrade pip

# dependencies from requirements file
RUN pip install -r /app/requirements.txt

# this bit is temporary for trying to solve the SklearnAPIClassifier|that didnt work
#RUN pip install --no-cache-dir adversarial-robustness-toolbox

#RUN python -c "from art.estimators.classification import scikitlearn; print(dir(scikitlearn))"

# Install local .whl package
RUN pip3 install --no-cache-dir /tmp/adversarial_robustness_toolbox-1.16.0-py3-none-any.whl
#RUN python -c "from art.estimators.classification import scikitlearn; print(dir(scikitlearn))"
# for the og directory with correct permissions
RUN mkdir -p /aicloud/logs && chmod -R 777 /aicloud/logs
# RUN ls -ltr /app/../*
# Expose port for FastAPI (default 8000)
EXPOSE 8000

# Start the application
CMD ["python3", "/app/app/main.py"]
