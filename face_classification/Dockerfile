# Use an official Debian runtime as a parent image
FROM debian:latest

# Set the working directory to /ekholabs/face-classifier
WORKDIR /ekholabs/face-classifier

# Update and install necessary packages
RUN apt-get update && apt-get install -y \
    git \
    python3 \
    python3-pip \
    python3-dev \
    python3-tk \
    vim \
    procps \
    curl

# Install Face classification dependencies & web application
RUN apt-get install -y python3-venv && \
    python3 -m venv /venv && \
    . /venv/bin/activate && \
    pip install --upgrade pip && \
    pip install numpy scipy scikit-learn pillow tensorflow pandas h5py opencv-python keras statistics pyyaml pyparsing cycler matplotlib Flask

# Copy the current directory contents into the container at /ekholabs/face-classifier
COPY . /ekholabs/face-classifier

# Set environment variables
ENV PYTHONPATH=$PYTHONPATH:src
ENV FACE_CLASSIFIER_PORT=8084
EXPOSE $FACE_CLASSIFIER_PORT

# Define the entry point
ENTRYPOINT ["python3"]
CMD ["src/web/faces.py"]