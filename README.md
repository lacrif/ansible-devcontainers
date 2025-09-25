# Ansible DevContainer

Un environnement de développement conteneurisé pour Ansible basé sur Python 3.12 et Debian Bookworm.

## Description

Ce DevContainer fournit un environnement de développement complet pour l'infrastructure as code avec Ansible. Il inclut tous les outils nécessaires pour développer, tester et valider vos playbooks et rôles Ansible.

## Fonctionnalités

### Outils inclus

- Ansible 11.0 
- Ansible Lint
- Docker
- YAML Lint
- Molecule
- Molecule Docker Plugin
- TestInfra

### Outils système

- OpenSSH Client
- Git
- Curl
- Certificats CA

## Utilisation

### Avec VS Code DevContainers

1. Clonez votre projet Ansible
2. Ajoutez ce Dockerfile dans un dossier .devcontainer/
3. Créez un fichier .devcontainer/devcontainer.json :

```json
{
    "name": "Ansible DevContainer",
    "image": "lacrif/ansible-devcontainer:11",
    "forwardPorts": [],
    "postCreateCommand": "ansible --version"
}
```

4. Ouvrez le projet dans VS Code
5. Cliquez sur "Reopen in Container" quand VS Code le propose

### Construction manuelle

```bash
# Construire l'image
docker pull lacrif/ansible-devcontainer:11

# Lancer le conteneur
docker run -it --rm -v $(pwd):/workspace lacrif/ansible-devcontainer:11 bash
```

### Structure de projet recommandée

```
projet-ansible/
├── .devcontainer/
│   └── devcontainer.json
├── inventories/
│   ├── development/
│   └── production/
├── playbooks/
├── roles/
├── molecule/
│   └── default/
├── ansible.cfg
└── requirements.yml
```

## Exemples d'utilisation

Vérifier l'installation

```bash
ansible --version
ansible-lint --version
molecule --version
```

Lancer un playbook

```bash
ansible-playbook -i inventories/development playbooks/site.yml
```

Tester avec Molecule

```bash
cd roles/mon-role
molecule test
```

Validation avec Ansible Lint

```bash
ansible-lint playbooks/
```

## Configuration

### Variables d'environnement utiles

`ANSIBLE_CONFIG` - Chemin vers le fichier de configuration Ansible
`ANSIBLE_INVENTORY` - Chemin par défaut vers l'inventaire
`ANSIBLE_PRIVATE_KEY_FILE` - Clé SSH privée par défaut

### Volumes recommandés

`/workspace` - Répertoire de travail principal
`~/.ssh` - Clés SSH (en lecture seule)
`~/.ansible` - Cache Ansible

## Auteur

[![Static Badge](https://img.shields.io/badge/Lacrif-0000?style=flat&logo=github&logoColor=white&color=black&link=https%3A%2F%2Fgithub.com%2Flacrif)](https://github.com/lacrif)
