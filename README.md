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

**1-5 Document your publication commands and published images in dockerhub**

![Capture d’écran du 2023-11-06 16-16-50](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/7213a9d5-d643-4dce-aba5-63756620f0c8)

**TP Part 02 :**

**2-1 What are testcontainers?**

Testcontainers est une bibliothèque Java qui permet d’instancier un conteneur Docker lors des tests. Testcontainers gère le cycle de vie des conteneurs, les démarrant avant l'exécution des tests et les arrêtant après leur fin. Cela permet aux tests d'être isolés, reproductibles et cohérents sur différents environnements.

**2-2 Document your Github Actions configurations**

Pour gérer mes github action configurations, j'ai réalisé deux fichier différents. Un premier qui s'occupe de tester le backend, et un deuxième qui se lance uniquement si le premier job passe, et qui permet de build et de push nos images docker. J'utilise un workflow dans le deuxième fichier pour gérer l'exécution à retardement.

- CI du back-end

![Capture d’écran du 2023-11-07 14-29-35](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/bef44164-915b-4c7c-8511-386e46f64141)

- CI docker

![Capture d’écran du 2023-11-07 14-31-24](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/ab40151d-a6c3-45ab-b3b6-a1ffae42c1df)

![Capture d’écran du 2023-11-07 14-32-07](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/b6c30526-2fc5-41e1-b76f-fab6a6097b21)

- Résultats

![Capture d’écran du 2023-11-07 14-37-17](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/6d52fef8-0132-45ba-84dc-49a06b4adf62)

![Capture d’écran du 2023-11-07 14-40-42](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/63975895-7d50-468a-9919-9a0ac9aa7f89)



**2-3 Document your quality gate configuration**

Pour obtenir une analyse dans sonarcloud de notre backend, on gère cela dans la CI du backend. On lance une commande maven permettant d'accéder à une organisation sonarcloud distante, en utilisant pour cela un token définit en secret sur notre github action.

![Capture d’écran du 2023-11-07 14-50-15](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/80b107d6-a339-4926-af6f-a58d9fa108a9)

![Capture d’écran du 2023-11-07 14-51-24](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/917a7b58-2820-4554-a414-5a9deebfe30f)

![Capture d’écran du 2023-11-07 14-47-23](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/b0a1023f-23e1-4ce8-a040-a84180c480ed)


**TP Part 03 :**

**3-1 Document your inventory and base commands**

![Capture d’écran du 2023-11-07 14-54-33](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/670064f6-adb9-4140-87fb-be8d4df0d4c0)

On test avec une commande de ping que tout fonctionne bien.

![Capture d’écran du 2023-11-07 15-38-19](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/f30604e4-6b3f-4083-b5a3-e3b7a34b19e7)

**3-2 Document your playbook**

![Capture d’écran du 2023-11-07 15-43-28](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/224a154c-1600-4249-b405-dbb284497dbb)

Ce fichier playbook permet de définir tous les roles que l'on va utiliser pour créer nos containers par la suite.

**3-3 Document your docker_container tasks configuration**

- Dans un premier temps on définit notre role docker qui permet de l'installer sur notre serveur et de le lancer.

![Capture d’écran du 2023-11-07 15-48-28](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/baa89606-0323-48c6-82ca-e5bece58a239)

- Ensuite on définit notre role network qui permet de créer un network comme fait dans la première partie du TP.

![Capture d’écran du 2023-11-07 15-54-14](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/e4536ffd-d318-4c7e-9994-5f8d79bc87d8)

- Ensuite on définit notre container qui permet de se connecter à notre database en définissant nos variables d'environnements.

![Capture d’écran du 2023-11-07 15-56-38](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/d519ae29-2d82-4865-957d-dd855f377bf7)

- Puis, on créé nos containers qui run le proxy, le back et le front.

![Capture d’écran du 2023-11-07 15-58-37](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/cb7e74de-6e1c-4499-a638-2863bc988a3e)

![Capture d’écran du 2023-11-07 15-59-02](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/4c77be9d-2617-4961-9ac6-cb84c3185de0)

![Capture d’écran du 2023-11-07 15-59-49](https://github.com/ALFONSI-jules/TP_DevOps/assets/73819497/e3c03171-b7b7-4544-8805-2c3c0664cf46)
