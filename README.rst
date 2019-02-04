script de sauvegarde
=====================

script de sauvegarde de données sur Amazon S3 grâce à la librairie BOTO3

installation
------------

L'installation de la dernière version de BOTO3 se fait avec PIP:

pip install boto3

configuration
-------------

avant de pouvoir utiliser ce module il faut d'abord parametrer son systeme avec les informations
d'authentification afin de pouvoir connecter son compte AWS avec la commande :
"aws configure".
cette commande vous nous permettre de renseigner les clés d'accès a notre compte AWS ainsi que
les paramètres régionaux.

AWS Access key ID [None]:
AWS Secret Access key [None]:
Default region name [None]:

toutes ces information sont disponible dans les paramètres de compte AWS.

utilisation
-----------

afin d'utilise boto3 il faut importer le module "import boto3"

et indiquer le service que nous voulons utiliser,afin d'accéder à notre bucket nous allons utiliser
la méthode boto3.resources('s3')

"s3 = boto3.ressource('s3')".

on peut ensuite interagir avec notre bucket en y sauvegardant des fichiers
s3_resource.Bucket(mon_bucket).upload_file(Filename="/chemin/nom_du_fichier,key=nom_du_fichier).

afin de lister le contenu du bcket utiliser la methode conn.list_object
for fichiers in conn.list_objects(Bucket=mon_bucket)['Contents']
