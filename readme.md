# Tutorial Aplicação
## Docker Swarm, Grafana, MySql, WordPress & Prometheus

1. Preparo para a excução
    1. Tenha o docker, git e WLS(Caso esteja no windows) instalados
    2. Verifique se as portas não estão sendo utilizadas

2. Criar o diretório
    1. Mkdir *Pasta*, cd *Pasta*
    2. git clone https://github.com/ArthurGNoronha/TrabalhoDocker
    3. cd TrabalhoDocker

3. Rode os seguintes comandos
    * docker stack deploy -c docker-compose.yml wordpress_stack
    * docker node ls
    * docker swarm init
    * docker node inspect -f '{{ .Status.Addr }} *Nome do Host*
    * docker ps
    * docker exec -it *id do container wordpress* bash
    * apt update
    * apt install nano
    * nano wp-config.php

    1. Adicione os seguintes comando entre as linhas
    ' if ($configExtra = getenv_docker('WORDPRESS_CONFIG_EXTRA', '')) {
        eval($configExtra);
        }

    /* That's all, stop editing! Happy publishing. */ '

    * define('WP_CACHE', true);
    * define('WP_REDIS_HOST', 'redis');
    * define('WP_REDIS_PORT', 6379);

    2. Utilize CTRL+X, Y e ENTER

4. Aproveitando que estamos dentro do container do WordPress, verifique o MYSQL
    * apt install default-mysql-client
    * mysql -h db -u wpuser -pwppassword wordpress
    * show tables;
    * CTRL+C
    * exit

5. Agora entre em http:// *ip da máquina lider*:80
    * Você deve ver essa imagem:
    |[Imagem do wordPress](../1.jpg)

    1. Agora entre em http:// *ip da máquina lider*:80/admin
    * Vá em "Tools", e então em "Info", e procure "Database"
        * Deve aparecer as configurações do BD
        |[Confirações do bd](../2.jpg)

    * Agora vá em "plugins" "Add New Plugin", procure o "Redis", instale e ative
        * Então vá em "Configurações" e "Redis", então inicie o Redis

6. Agora entre em http:// *ip da máquina lider*:9090
    * Digite "up" na aba "Expressions" e rode em "Execute"
    * Então veja as instancias que estão rodando

7. Vá em http:// *ip da máquina lider*:3000
    1. Faça o Login utilizando "Admin" e "Admin"
    2. Vá em Data sources
        1. "Add new data source"
        2. Selecione o Prometheus
        3. Na aba de conection coloque http:// *ip da máquina lider*:9090
        4. Clique em Save e Test

8. Agora vá em "dashboards" "New" e "Import"
    * Importe um código, como por exemplo '3662', e de um Import

9. Agora vá em http:// *ip da máquina lider*:9090/Targets e se as aplicações estão rodando  com sucesso

# Fim.

## Arthur Noronha