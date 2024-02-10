FROM pytorch/pytorch:2.1.0-cuda11.8-cudnn8-runtime

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=1 \
    PIP_DEFAULT_TIMEOUT=100 \
    C_FORCE_ROOT=true \
    DEBIAN_FRONTEND=noninteractive \
    START_FILE_PATH=deployment/start.sh \
    REQUIREMENTS_PATH=requirements.txt

RUN apt-get update \
    && apt-get install -y ca-certificates software-properties-common build-essential wget git \
                          texlive texlive-latex-extra texlive-xetex pandoc \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /home/jovyan

RUN useradd -u 1317 -d /home/jovyan -s /bin/bash jovyan
WORKDIR /home/jovyan

COPY ${START_FILE_PATH} /usr/local/bin/start.sh
RUN chmod 777 /usr/local/bin/start.sh

RUN pip install --upgrade pip setuptools

COPY ${REQUIREMENTS_PATH} requirements.txt
RUN pip install --upgrade -r requirements.txt

USER jovyan