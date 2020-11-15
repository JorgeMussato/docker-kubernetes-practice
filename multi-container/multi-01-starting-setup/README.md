Como colocar os blocos em containeres separados e funcionais.

1 - Criar duas networks:
docker network create net_web
docker network create net_db

2 - Subir container do MongoDB em volume mapeado:
docker container run --name mongo_db --network net_db --rm -v multi-app-db:/data/db -d mongo

3 - Subir o container do back end:
docker build -t goals-node . 

docker container run --name nodeapp --rm -d -v "D:/Programacao/devops/Docker/multi-container/multi-01-starting-setup/backend:/app" -v logs:/app/logs -v /app/node_modules --network net_db goals-node

docker network connect net_web nodeapp

4 - Subir o container do front end