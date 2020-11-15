Como colocar os blocos em containeres separados e funcionais.

1 - Criar network:
docker network create net_db

2 - Subir container do MongoDB em volume mapeado:
docker container run --name mongo_db --network net_db --rm -v multi-app-db:/data/db -e MONGO_INITDB_ROOT_USERNAME=jorge -e MONGO_INITDB_ROOT_PASSWORD=secret -d mongo

3 - Subir o container do back end:
docker build -t goals-node . 

docker container run --name nodeapp --rm -d -v "D:/Programacao/devops/Docker/multi-container/multi-01-starting-setup/backend:/app" -v logs:/app/logs -v /app/node_modules --network net_db -e MONGODB_USERNAME=jorge -e MONGO_DB_PASSWORD secret goals-node

4 - Subir o container do front end (precisa do -it por ser React). React não permite usar nome de containers em URL por rodar no navegador e não dentro do servidor do container
docker run --name reactapp -p 3000:3000 -d --rm -it -v D:/Programacao/devops/Docker/multi-container/multi-01-starting-setup/frontend/src:/app/src goals-react

Para visualizar mudanças em real time do REACT devemos usar o sistema de pastas do LINUX dentro do windows (usuarios de WSL2), verificar arquivo PDF em anexo.