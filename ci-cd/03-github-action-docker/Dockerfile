# Start with an official Python runtime as the base image
FROM python:3.10-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container
COPY . /app

# Install any dependencies
RUN pip install -r requirements.txt

# Run the application
CMD ["python", "-m", "unittest", "discover"]
