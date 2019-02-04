#!/usr/bin/env python3.6

# importation de la librairie boto3
import boto3

# Importation du module datetime pour inscrire la date et l'heure d'éxècution du script
from datetime import datetime
import time

# On declare le service AWS auquel on souhaiterais accéder
s3_resource = boto3.resource('s3')

# On déclare le nom du bucket AWS dans lequel on veut sauvegarder les fichiers
mon_bucket = "monprojet4"

# On determine le moment du début de l'execution de la savegarde
début = time.time()

# Methode de chargement d'un fichier dans le bucket par son nom
s3_resource.Bucket(mon_bucket).upload_file(Filename="/home/adminsys/mes_fichiers/fichier_test.txt"\
,Key="fichier_test.txt")

# On determine le moment de la fin de la sauvegarde
fin = time.time()

# On affiche un message indiquant la fin de la sauvegarde
print("-------------------------------------")
print("fichier sauvegardé sur s3 avec succès")
print("-------------------------------------")

#On affiche un message indiquant le temps de la sauvegarde
print(f"Temps de chargement: {fin - début} secondes")
print("-------------------------------------")

# On affecte la variable conn afin de nous connecter à notre bucket sur s3
conn = boto3.client('s3')

# On utilise la boucle While afin d'imposer une reponse pour la demande d'affichage du contenu
# du bucket
while True:

# On capture la variable affichage
	affichage = input("Voulez vous afficher le contenu actuel de votre bucket?(o/n) :")

# Bloc try combiné d'une erreur d'assertion que je vais moi même créer
	try:

# On vérifit la lettre tapée
		assert affichage == "o" or affichage=="n"

# Ce que l'on demande d'afficher en cas de non respect de la lettre demandée
	except AssertionError:
		print("Veuillez entrer o ou n")

# Mot clé permettant de retourner au while afin de reposer la question
		continue

# Sinon si l'utilisateur tape o on demande l'affichage du contenu du bucket gràce a la boucle for
# qui va parcourir chaque élèment,l'inclure dans une variable nommée fichier et l'afficher
# grâce à la methode list_object
	else:
		if affichage == "o":

			for fichiers in conn.list_objects(Bucket=mon_bucket)['Contents']:
				print(fichiers['Key'])

# On demande l'arrêt de la boucle avec le mot-clé "break"
			break

# Sinon l'utilisateur a tapé "n" et l'on affiche "fin du traitement"
		else:
			print("** fin du traitement **")
			break

# On inscrit la date d'execution du script ainsi que le temps de chargement dans un fichier 
f = open("date_execution.txt","a")
f.write(f"Fcihier sauvegardé le : {datetime.now()} en {fin-début} secondes\n")
f.close()
