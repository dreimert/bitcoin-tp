# TP3 - Minage Bitcoin

L'objectif du TP est de modifier le code source de bitcoin pour y créer sa propre *blockchain* et voir le minage en fonctionnement.

## Etapes préliminaires

La dernière version des outils a retiré le principe de minage pour des raisons d'utilité. Si vous voulez tester les principes du minage il ne faut pas utiliser la version la plus récente des outils.
La dernière version à supporter le minage est la v0.12.0.

#### Q1 : Que fait `git tag` ?

#### Q2 : Que fait `git checkout` ?

#### Q3 : Quelle commande git vous permet de travailler sur la v0.12.0 de bitcoin ?

Une fois la version récupérée vous devez (re)compiler vos outils. Il faudra certainement (re)passer par une phase de reconfiguration.

#### Q4 : Où est la documentation pour compiler bitcoin ?

#### Q5 :  D'un point de vue minage que se passe t'il au lancement du démon ?

Si on veut utiliser notre propre blockchain, il faut manipuler les sources du système. La configuration de la blockchain se situe dans le fichier src/chainparams.cpp.

Ouvrez et parcourez rapidement ce fichier.

Le code suivant permet d'écrire dans la console en c++ :

    #include <iostream>
    std::cout << strMytestString;

#### Q6 : Ajouter une trace quelconque dans le fichier pour vérifier que vos modifications sont bien prises en compte. Recompilez et exectuez le demon.

#### Q7 : Tester la fonction de minage avec l'appel CLI : setgenerate true

Modification des paramètres de lancement
La première étape est de ne plus se connecter au réseau Bitcoin.

#### Q8 : Quel mode permet de lancer bitcoind sans qu'il se connecte à d'autres noeuds noeuds ?

#### Q9 : La configuration de ce paramètre est dans le fichier src/chainparams.cpp. Que fait-il avec les seeds du réseau ? (Qu'est ce qu'un seed dans un réseau ?)

#### Q10 : La configuration du réseau principal est aussi définis dans src/chainparams.cpp. Quels sont les seeds proposés ?

Faite en sorte que la chaîne principale ne se connecte plus au réseau Bitcoin.

Arrêtez, recompiler, nettoyer votre dossier de configuration et relancer le demon.
Par la suite, quand on parle de relancer, on s'attend à ce que vous fassiez les actions de la phrase précédente.

#### Q11 : Que ce passe t'il ? Pouvez vous désactiver cette tâche répétitive ?

Nous sommes maintenant isolés du réseau mainnet officiel.

#### Q12 : Comment s'appelle le premier block à la chaine ?

#### Q13 : Quelle fonction sert à le calculer ?

#### Q14 : Que représentent les parametres de la fonction ?

#### Q15 : Que signifie nonce ?

Modifier certaines valeurs et relancer.

#### Q16 : Que se passe t'il ? Pourquoi ?

Corrigez la ligne et relancer.

#### Q17 : Que se passe t'il ? Pourquoi ?

Il faut donc trouver un hash acceptable. Il va donc falloir tester plusieurs blocks en changeant le nonce, jusqu'à trouve un hash valide. C'est exactement ce qu'un mineur réalise comme fonction.

Dans les includes du fichiers, ajouter : #include "arith_uint256.h"

Et remplacer la creation du premier block de la chaine par :

    arith_uint256 targetGenesisBlockDifficulty = arith_uint256("0x00000000ffffffffffffffffffffffffffffffffffffffffffffffffffffffff");
    unsigned int tmp = 0;
    genesis = CreateGenesisBlock(1231006505, tmp, 0x1d00ffff, 1, 50 * COIN);
    for(; UintToArith256(genesis.GetHash()) > targetGenesisBlockDifficulty; tmp++){
      genesis = CreateGenesisBlock(1231006505, tmp, 0x1d00ffff, 1, 50 * COIN);
      printf("Block Testé %d -> %s\n", tmp, genesis.GetHash().ToString().c_str());
    }

#### Q18 : Que fait ce code ?

Relancer.

#### Q19 : Que se passe-t-il ?

Afin d'avoir une réponse plus rapide, il faut agir sur deux paramètres. La difficulté minimale que le système peut rencontrer et la difficulté minimale du genesis block.

Modifiez le code pour indiquer une difficulté minimale de :
'0000ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff'

#### Q20 : Quelle était la difficulté précédente ?

Maintenant il faut baisser la difficulté pour le choix du block génésis.

En lisant cette entrée de stackexchange, http://bitcoin.stackexchange.com/questions/30467/what-are-the-equations-to-convert-between-bits-and-difficulty...

1- Validez le fait que
0x00000000ffffffffffffffffffffffffffffffffffffffffffffffffffffffff == 0x1d00ffff
2 - Corrigez le script de recherche du block genesis pour avoir une diffulté inférieure à la difficulté minimale.

#### Q21 : Que ce passe t'il ?

Si vous voulez testez vos compétences techniques, n'allez pas à la question suivante, mais essayez de tracer le code pour comprendre pourquoi le minage ne s'exécute pas.
SINON VOUS POUVEZ LIRE LA SUITE

Vous êtes sur ?

Certain ?

Vous ne voulez vraiment pas essayer avant ?

Prenez le temps d'essayer de comprendre ?

Discutez-en avec votre voisin....

Si vous passez cette ligne, vous n'aurez pas transpiré devant votre code. Est-ce vraiment ce que vous désirez ?

Bon ok
Pour lancer notre nouvelle blockchain, reportez-vous au tp précédent pour connecter deux noeuds. Relancer.

Les deux doivent se connecter mais ensuite il ne se passe rien.

Il y a deux vérification qu'il faut supprimer pour que la chaine se lance. Il faut supprimer les checkpoints qui servent à vérifier la blockchain bitcoin :

    checkpointData = (CCheckpointData) {
      boost::assign::map_list_of
      ( 0, uint256S("0x0000000069e244f73d78e8fd29ba2fd2ed618bd6fa2ee92559f542fdb26e7c1d")),
      0, // * UNIX timestamp of last checkpoint block
      0,   // * total number of transactions between genesis and last checkpoint
                        //   (the tx=... number in the SetBestChain debug.log lines)
      0.0     // * estimated number of transactions per day after checkpoint
    };

et changer le timestamp dans la generation du premier block (1473068827) par le timestamp courant. Le dernier block de la blockchain doit avoir moins de 24h. Relancer.

http://web2.0calc.com/ vous donne une calculatrice de conversion de date.

Refs :
http://dillingers.com/blog/2015/04/18/how-to-make-an-altcoin/
https://geraldkaszuba.com/creating-your-own-experimental-bitcoin-network/
https://github.com/coinclone/cloner
