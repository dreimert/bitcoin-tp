# TP Bitcoin

## Docker

### Créer et lancer le conteneur

    docker create -it --name mybitcoin  dreimert/bitcoin-tp bash
    docker start -ai mybitcoin
    
### Lancer un terminal supplèmentaire

    docker ps
    docker exec -it <CONTAINER ID ou container name>

## Vous êtes dans le conteneur

Du coup, vous pouvez suivre la première version de ce TP jusqu'à la question 17 : https://sfrenot.jumplyn.com/tp3-minage-bitcoin/
