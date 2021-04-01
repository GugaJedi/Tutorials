# TUTORIAL

## Instalação de Servidor Zanthus para Ambiente Cloud

# SETUP

1. Usuários
    ```sh
    useradd -r zanthus; useradd postgres
    ```
1. Diretórios
    ```sh
    cd /; mkdir backup infra web data; cd /infra; mkdir _env libs logs pacotes tmpz utils primeshare; mkdir -p /Zanthus/Zeus/Manager
    ```
    1. permissões de diretórios
    ```
    chown -fR zanthus.zanthus /Zanthus
    ```
2. 
