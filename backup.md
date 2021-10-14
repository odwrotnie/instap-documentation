# Backup

## Zatrzymanie aplikacji

```
docker-compose stop
```

## Backup aplikacji

```
docker save -o recipesfortasks.gz recipesfortasks:latest 
docker save -o validator.gz validator:latest 
docker save -o recipesforreservations.gz recipesforreservations:latest
docker save -o recipesforreports.gz recipesforreports:latest 
docker save -o recipesforfields.gz recipesforfields:latest 
docker save -o cronldap.gz cronldap:latest  
docker save -o relations.gz relations:latest
docker save -o plots.gz plots:latest 
docker save -o misc.gz misc:latest  
docker save -o gateway.gz gateway:latest   
docker save -o defitems.gz defitems:latest
docker save -o exports.gz exports:latest 
docker save -o users.gz users:latest 
docker save -o notes.gz notes:latest 
docker save -o web-app_node_red.gz notes:latest 
docker save -o files.gz
docker save -o web-app_superset.gz web-app_superset 
docker save -o web-app_webapp.gz web-app_webapp  
docker save -o instap_postgraphile.gz instap_postgraphile 
```

## Backup bazy danych

```
docker exec InstapDatabase pg_dump -U app db > database_$(date +%Y-%m-%d_%H:%M:%S).sql
```

# Restore

## Czyszczenie bazy

```
docker exec InstapDatabase dropdb app
```

## Ładowanie danych z backupu

```
cat database<date>.sql | docker exec -i InstapDatabase psql -U app db
```

## Start kontenerow

```
docker load -i recipesfortasks.gz 
docker load -i validator.gz 
docker load -i recipesforreservations.gz
docker load -i recipesforreports.gz 
docker load -i recipesforfields.gz 
docker load -i cronldap.gz  
docker load -i relations.gz
docker load -i plots.gz 
docker load -i misc.gz   
docker load -i gateway.gz 
docker load -i defitems.gz  
docker load -i exports.gz 
docker load -i users.gz 
docker load -i notes.gz 
docker load -i web-app_node_red.gz
docker load -i files.gz
docker load -i web-app_superset.gz 
docker load -i web-app_webapp.gz  
docker load -i instap_postgraphile.gz

docker-compose up -d
```
