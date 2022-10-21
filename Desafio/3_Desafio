# Exercicios

### 1 Crie um container com as seguintes características:
* Crie uma pasta em seu desktop e nele crie um arquivo chamado index.html e nele construa uma pagina com um hello world!
* A imagem que deve ser utilizada é httpd:2.4 (apache) ;
* O nome do container deve ser apache;
* Executa-lo em modo daemon;
* Faça o redirecionamento de porta 8080 para 80;

```
docker run --name apache -d -p 8080:80 httpd:2.4
```

* Faça o mapeamento da pasta que você criou com o arquivo index.html para dentro do container (local dentro do container: /usr/local/apache2/htdocs/);

```
docker exec -it apache /bin/bash
```

* Exponha o valor definido na variável de ambiente PORT para que os usuários do contêiner saibam como acessar o Apache Web Server;
* Com a pasta criada no seu desktop e dentro dela o arquivo index.html, o arquivo deve ser copiado para a pasta do Apache DocumentRoot (/var/www/html/) dentro do container.

Não existia o caminho /var/www/html/. Então a pasta que eu criei no meu desktop se chamava www e dentro dela outra com o nome html que contém o arquivo index.html

```
docker cp ./www apache:/var
```
  

### 2 Apos o container executado utilize o comando curl ou o seu navegador para acessar o arquivo index.html que foi criado.



