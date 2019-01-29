script de sauvegarde
=====================

script de sauvegarde de données sur Amazon S3 grâce à la librairie BOTO3

Installation
------------

L'installation de la dernière version de BOTO3 se fait avec PIP:

pip install boto3

Configuration
-------------

Avant de pouvoir utiliser ce module il faut d'abord parametrer son systeme avec les informations
d'authentification afin de pouvoir connecter son compte AWS avec la commande :
"aws configure".
Cette commande vous nous permettre de renseigner les clés d'accès a notre compte AWS ainsi que
les paramètres régionaux.
Toutes ces information sont disponible dans les paramètres de compte AWS.

Utilisation
-----------

Afin d'utilise boto3 il faut importer le module "import boto3"
Et indiquer le service que nous voulons utiliser,afin d'accéder à notre bucket nous allons
utiliser s3 "s3 = boto3.ressource('s3')".
On peut ensuite interagir avec notre bucket en telechargeant ou en y sauvegardant des fichier.

