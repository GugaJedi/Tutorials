# AMBIENTE ZAPP - UPLOADER

## CRIANDO NOVO AMBIENTE

### PREPARANDO O UPLOADER

1. configure o .env de acordo com as informações do banco do cliente e rode o script abaixo em TODOS os servidores de APP apache.

rm -rf vendor && \
    chmod 777 -R storage && \
    ./composer.phar install && \
    php artisan config:clear && \
    php artisan clear-compiled && \
    php artisan config:cache && \
    ./composer.phar dump-autoload
	
2. para preparar o banco de dados rode o comando abaixo APENAS EM UM dos servidores de aplicação.

php artisan migrate:refresh --seed

## ATUALIZANDO O UPLOADER

1. Descompacte o pacote enviado no diretório onde já esta instalado, mas lembre-se de remover do *.zip o arquivo .env para não substituir o existente e rode o script abaixo em TODOS os servidores de APP apache.

rm -rf vendor && \
    chmod 777 -R storage && \
    ./composer.phar install && \
    php artisan config:clear && \
    php artisan clear-compiled && \
    php artisan config:cache && \
    ./composer.phar dump-autoload