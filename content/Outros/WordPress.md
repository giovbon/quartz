---
title: WordPress
---
É um Sistema de Gerenciamento de Conteúdo (CMS). Criado para ser modificado e expandido, permite a criação de muitas coisas. Suporte a themes e plugins. Tem licença GNU / GPL, permitindo que modifique qualquer coisa no software, é completamente gratuito.

- Para autohospedar: [Ferramenta de blog, plataforma de publicação e CMS – WordPress.org Brasil](https://br.wordpress.org/)
- Do cara que criou o video: [WP Course Tools](https://wpcoursetools.com/)  

- Coisas que possuem custo para publicar website
	- Domain Name (por ano)
    - Conta de hospedagem (depende do tráfego que o site tem
- Se for autohospedar nos seu pc, podes criar sites e se familiarizar com a ferramenta, mas o site não ficará disponível na web

Consegui instalar via docker-compose:

```yaml
# https://github.com/docker/awesome-compose/blob/master/official-documentation-samples/wordpress/README.md

# acesse http://localhost/wp-admin/ ou http://localhost:80

services:
  db:
    # We use a mariadb image which supports both amd64 & arm64 architecture
    image: mariadb:10.6.4-focal
    container_name: wordpress_db
    # If you really want to use MySQL, uncomment the following line
    #image: mysql:8.0.27
    command: '--default-authentication-plugin=mysql_native_password'
    volumes:
      - db_data:/var/lib/mysql
    restart: unless-stopped
    environment:
      - MYSQL_ROOT_PASSWORD=somewordpress
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=wordpress
    expose:
      - 3306
      - 33060
  wordpress:
    container_name: wordpress
    image: wordpress:latest
    volumes:
      - wp_data:/var/www/html
    ports:
      - 80:80
    restart: unless-stopped
    environment:
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
volumes:
  db_data:
  wp_data:
```

- Instalação em web host [https://www.youtube.com/watch?v=09gj5gM4V98&t=1565s](https://www.youtube.com/watch?v=09gj5gM4V98&t=1565s)

- [ ] TODO [https://youtu.be/09gj5gM4V98?t=1566](https://youtu.be/09gj5gM4V98?t=1566)