**# TP_DevOps**
Rapport TP DevOps

**TP Part 01 :**

**1-1 Document your database container essentials: commands and Dockerfile**

- Premièrement, on créé un fichier 01-CreateScheme.sql dans lequel on créé les Tables de notre base de données.

![Capture d’écran du 2023-11-06 13-59-48](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/e724d811-0794-4994-87ed-ef19dbca3522)

                                                              
- Deuxièmement, on créé un fichier 02-InsertData.sql afin d’insérer des données dans notre BDD.

![Capture d’écran du 2023-11-06 14-02-37](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/803137bd-8a60-4182-877b-84cf8fc457d7)

- Ensuite on créé un fichier Dockerfile dans lequel on va récupérer l’image postgres de docker, et on se sert de ce fichier pour définir différentes variables d’accès à notre base de données telles que db, user et password.

![Capture d’écran du 2023-11-06 14-05-52](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/6a0449fe-c66b-474e-b845-7d5516a03cce)


- Une fois le dockerfile créé, on créé un network que l’on utilisera par la suite dans chacun de nos containers

![Capture d’écran du 2023-11-06 14-11-05](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/3f3494cb-7ab2-403e-a3e1-4f9870451706)

 
- On run le container de adminer permettant d’accéder aux informations de la base de données depuis le port 8090 de notre localhost. On build également notre image afin de l’utiliser dans le container de notre database.

![Capture d’écran du 2023-11-06 14-12-22](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/825ae296-2c30-4b8d-8b97-508277e422e5)

 
- Enfin on run le container de notre base de données, à partir de l’image que l’on a build précédemment. On utilise un volume afin de sauvegarder nos données même lorsque l’on kill nos containers.

![Capture d’écran du 2023-11-06 14-21-03](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/9545de62-fe1f-4116-9ec8-c41ca287ef21)

 
- Enfin, on peut visualiser notre bdd depuis adminer en se connectant, avec les variables définies dans notre dockerfile.

![Capture d’écran du 2023-11-06 14-21-44](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/10b103fb-bc50-4831-838b-43e2f4ea4383)


**1-2 Why do we need a multistage build? And explain each step of this dockerfile**

Le multistage build permet de créer des images Docker plus efficaces et plus petites en divisant le processus de construction en plusieurs étapes. Chaque étape produit une image intermédiaire, dans laquelle on copie uniquement les fichiers nécessaires. Cela aide à réduire la taille de l'image finale en excluant les dépendances de construction, les fichiers intermédiaires et les outils inutiles.

![Capture d’écran du 2023-11-06 14-59-11](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/e1ef3eef-9f93-4a64-b834-9846d64533af)


Etape build :

On importe d’abord une image maven pour cette étape. On définit ensuite une variable d’environnement pour stocker les fichiers de l’application dans le container. On définit notre répertoir de travail. On copie ensuite le fichier pom.xml dans le répertoire de travail du container. On copie le code source dans le répertoire src du container. Enfin, on build avec une commande maven qui permet de skip les tests pendant le build.

Etape run :

On importe d’abord une image java. On définit une nouvelle fois une variable d’environnement et le répertoire de travail. Ensuite on copie le fichier JAR résultant de l'étape de construction dans le répertoire de travail du container. Enfin, on spécifie la commande par défaut à exécuter lorsque le conteneur démarre. 

**1-3 Document docker-compose most important commands**

- Docker compose up permet de démarrer tous les containers présents dans le fichier docker compose

- Docker compose down permet de stopper et supprimer tous les containers en cours qui sont dans le fichier docker compose.

- Docker compose build permet de reconstruire les images des différents containers contenus dans le fichier docker compose.

**1-4 Document your docker-compose file** 


![Capture d’écran du 2023-11-06 15-57-10](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/1738c994-1fa8-48d5-b4d8-d5064967ee70)
![Capture d’écran du 2023-11-06 15-57-41](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/dc814630-b325-40f8-955a-6297efcd927c)


Ce fichier docker compose permet de définir tous les containers et networks dans un seul et même fichier. On créé ainsi des services indiquant où trouver les différents dockerfile avec le contexte, le nom du container, le port sur lequel on l’expose, le network si nécessaire et les autres services dont les containers peuvent dépendre.

1-5 Document your publication commands and published images in dockerhub

