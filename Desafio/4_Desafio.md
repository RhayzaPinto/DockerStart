# Exercicio - O exercicio devera ser feito em duplas que serao escolhidas por mim.

### 1 Provisione uma aplicacao e persista os dados dela. Vamos utilizar neste exercicio o docker-compose.
* Crie uma pasta para conter a estutura do seu projeto;
* Neste exercicio vamos utilizar uma aplicacao em python e um redis;
* Crie um arquivo chamado app.py e nele insira o codigo abaixo:
```
import time
import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)

```
Arquivo requirements.txt

```
flask
redis
```

* Crie um arquivo Dockerfile e nele voce ira utilizar a seguinte estrutura:

```
# syntax=docker/dockerfile:1

FROM python

WORKDIR /src

ENV FLASK_APP=app.py

ENV FLASK_RUN_HOST=0.0.0.0

RUN apk add --no-cache gcc musl-dev linux-headers

COPY requirements.txt requirements.txt

RUN pip install -r requirements.txt

EXPOSE 5000

COPY . .

CMD ["flask", "run"]
```

* Crie um arquivo docker-compose.yml. Nele voce deve ter a estrutura para que seja feita o build da sua aplicacao e suba junto uma outra aplicacao que o redis;

* Para facilitar segue a estrutura inicial do docker-compose. Voce precisa inserir os itens faltantes:

```
version: '3.8'
services:
  web:
 
    ports:
      - "8000:5000"
  redis:
    image: redis
    ports:
      - '6379:6379'

    volumes: 
      - ./cache:/data
volumes:
  cache:
    driver: local
```

* Fique bem atento pois estao faltando varias declaracoes para que suba a sua aplicacao em python e o redis que devem serem executados. Repare que existe uma declaracao de volume. Isso significa que os dados do redis serao armazenados e mesmo que o container se encerre os dados nao serao perdidos;

* Após a construção do arquivo, execute o comando necessário para que realize o build da aplicação e então suba os dois serviços;

```
docker build -t rhayzapinto/meudockerfile .
docker-compose up -d
```

* Repare que a cada refresh no seu navegador o numero e modificado;

* Execute o comando para baixar os dois servicos e entao suba novamente o docker-compose e veja se o numero permanece o mesmo ou ele inicia a partir do 1. Se iniciar a partir do 1 ele estara errado. E necessario rever a parte do volume do seu docker-compose.