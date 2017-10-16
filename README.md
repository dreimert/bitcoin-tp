# TP Bitcoin

## Docker

### Créer et lancer le conteneur

    docker create -it --name mybitcoin  dreimert/bitcoin-tp bash
    docker start -ai mybitcoin
    
### Lancer un terminal supplèmentaire

    docker ps
    docker exec -it <CONTAINER ID ou container name> bash
    
### Mettre à jour l'image

    docker pull dreimert/bitcoin-tp

## Vous êtes dans le conteneur

Du coup, vous pouvez suivre la première version de ce TP jusqu'à la question 17 : https://sfrenot.jumplyn.com/tp3-minage-bitcoin/

## Docker le retour

### Créer une image à partir d'un container

    docker commit <CONTAINER ID ou container name> bash

### Obtenir l'ip d'un container

    docker inspect <CONTAINER ID ou container name> | grep IPAddress
