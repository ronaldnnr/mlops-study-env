#estudos #mlops 
# MLOps Env Study

Ambientes para fins de estudos.

Os seguintes serviços serão executados:

1. MLflow
2. Airflow with Celery Executor
    - user: airflow
    - pass: airflow
3. Vault
    - token: myroot
4. PostgreSQL {Airflow e MLFlow}
5. Redis
6. Adminer
    - Airflow:
        - Server: postgres_airflow
        - User: airflow
        - Pass: airflow
    - MLFLow
        - Server: postgres_mlflow
        - User: mlflow
        - Pass: mlflow

Obs.: Credencias podem ser alteradas no arquivo `docker-compose.yml`

## Comandos úteis para iniciar os serviços do docker-compose:

1.  `docker-compose up`: Este comando inicia os contêineres definidos no arquivo `docker-compose.yml`. Se os contêineres ainda não foram construídos, eles serão construídos antes de serem iniciados. Você pode usar a opção `-d` para executar os contêineres em segundo plano.
    
2.  `docker-compose down`: Este comando para e remove os contêineres definidos no arquivo `docker-compose.yml`. Isso também remove todas as redes e volumes criados pelo comando `up`. Use a opção `-v` para remover também volumes criados pelos contêineres.
    
3.  `docker-compose ps`: Este comando lista os contêineres em execução definidos no arquivo `docker-compose.yml`.
    
4.  `docker-compose logs`: Este comando exibe as saídas dos logs dos contêineres em execução definidos no arquivo `docker-compose.yml`. Use a opção `-f` para acompanhar a saída dos logs em tempo real.
    
5.  `docker-compose build`: Este comando constrói as imagens dos contêineres definidos no arquivo `docker-compose.yml`. Use a opção `--no-cache` para ignorar o cache do Docker ao construir as imagens.
    
6.  `docker-compose exec`: Este comando executa um comando em um contêiner em execução definido no arquivo `docker-compose.yml`. Use a opção `-T` para desabilitar alocação de terminal.
    
7.  `docker-compose pull`: Este comando puxa as imagens mais recentes dos repositórios de imagens do Docker definidos no arquivo `docker-compose.yml`. Use a opção `--ignore-pull-failures` para continuar puxando outras imagens, mesmo que uma delas falhe.

## Acessando os serviços:
- Airflow: http://127.0.0.1:8080/
- MLFlow: http://127.0.0.1:5000/
- Vault: http://127.0.0.1:8200/
- Adminer: http://127.0.0.1:8081/

## Subir serviços durante inicialização:

`Linux`

- Crie o arquivo `docker-compose-mlops.service` no diretório `/etc/systemd/system/`  com o comando abaixo:

```bash
sudo vim /etc/systemd/system/docker-compose-mlops.service
```

Comando:
```txt
[Unit]
Description=Docker Compose Service MLOps
Requires=docker.service
After=docker.service

[Service]
TimeoutStartSec=0
RemainAfterExit=yes
Type=oneshot
WorkingDirectory={dir_docker_compose}/mlops-env
ExecStart=/usr/local/bin/docker-compose up -d
ExecStop=/usr/local/bin/docker-compose down
User=gustavo
Group=gustavo

[Install]
WantedBy=multi-user.target
```

- Recarregue as unidades do Systemd
```bash
systemctl daemon-reload
```

- Habilitando o serviço para iniciar junto do S.O:
```bash
systemctl enable docker-compose-mlops.service
```

`Created by Gustavo Oliveira`
