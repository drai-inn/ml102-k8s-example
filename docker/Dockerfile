# One of the datasets is no longer downloadable so need to copy it from an old image
FROM ghcr.io/nesi/training-environment-jupyter-ml102-app:v0.3.0 AS source

# Using an older version as ML102 notebooks haven't been updated in a long time
FROM nvcr.io/nvidia/tensorflow:24.01-tf2-py3

# install system dependencies
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    curl \
    git \
    locales \
    less \
    nano \
    nodejs \
    rsync \
    unzip \
    vim \
    wget \
    zip \
    && rm -rf /var/lib/apt/lists/*  \
    && localedef -i en_NZ -c -f UTF-8 -A /usr/share/locale/locale.alias en_NZ.UTF-8

ENV LANG=en_NZ.UTF-8

# Copy the cats_and_dogs_filtered dataset from the source image
COPY --from=source /var/lib/cats_and_dogs_filtered /var/lib/cats_and_dogs_filtered

# download flower photos
RUN wget -nv https://storage.googleapis.com/download.tensorflow.org/example_images/flower_photos.tgz \
    -O /var/lib/flower_photos.tgz \
    && tar -xzf /var/lib/flower_photos.tgz -C /var/lib \
    && rm -f /var/lib/flower_photos.tgz \
    && chown -R root:root /var/lib/flower_photos \
    && chmod -R o+rX /var/lib/flower_photos \
    && chown -R root:root /var/lib/cats_and_dogs_filtered \
    && chmod -R o+rX /var/lib/cats_and_dogs_filtered

# Copy workshop code
COPY ml102_workshop /opt/ml102_workshop
WORKDIR /opt/ml102_workshop

# install python dependencies
RUN python -m pip install --no-cache-dir \
    ipywidgets \
    matplotlib \
    pillow \
    tensorflow-datasets
