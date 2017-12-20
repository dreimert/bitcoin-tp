# TP Bitcoin

## Docker

### Télécharger, créer et lancer le conteneur

    docker pull dreimert/bitcoin-tp
    docker create -it --name mybitcoin  dreimert/bitcoin-tp bash
    docker start -ai mybitcoin
    
### Lancer un terminal supplèmentaire

    docker ps
    docker exec -it <CONTAINER ID ou container name> bash
    
### Mettre à jour l'image

    docker pull dreimert/bitcoin-tp

## Vous êtes dans le conteneur

Du coup, vous pouvez passer au TP lui-même : [TP](./TP3.md)
## Docker le retour

### Créer une image à partir d'un container

    docker commit <CONTAINER ID ou container name> bash

### Obtenir l'ip d'un container

    docker inspect <CONTAINER ID ou container name> | grep IPAddress
