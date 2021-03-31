# SETUP

1. Configuração da EC
   1. Particionamento
        - EBS 32 GiB
        - NFS mount \infra
        - NFS mount \backup
   1. Diretórios
        - root (/)
            ```
                cd /
                mkdir backup infra web data
                cd /infra
                mkdir _env libs logs pacotes tmpz utils primeshare
            ```
   1. Usuários
         - postgres
            ```
                useradd -r zanthus
            ```
         - zanthus
            ```
                useradd postgres
            ```
