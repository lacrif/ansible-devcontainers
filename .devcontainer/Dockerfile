FROM mcr.microsoft.com/devcontainers/python:3.12-bookworm

# Metadata
LABEL maintainer="Lacrif"
LABEL description="Ansible is a suite of software tools that enables infrastructure as code."
LABEL version="11"

# Installation et nettoyage en une seule couche pour minimiser la taille
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        openssh-client \
        git \
        curl \
        ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Active l'environnement virtuel et installe Ansible
RUN python3 -m pip install --no-cache-dir \
        ansible~=11.0 \ 
        ansible-lint \
        docker \
        yamllint \
        molecule \
        molecule-plugins[docker] \
        testinfra

# Point d'entrée
CMD ["ansible", "--version"]