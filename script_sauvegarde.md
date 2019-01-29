#!/usr/bin/env python3.6

# importation de la librairie boto3

import boto3

from datetime import datetime

# Renseignement du service AWS auquel je souhaiterais accéder
s3_resource = boto3.resource('s3')

# Affectation des variables clés d'accès afin de se connecter automatiquement au compte AWS
ACCES_KEY_ID = "AKIAJD77J7MUBAVEACZQ"

ACCESS_SECRET_KEY = "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"

# Renseignement du nom du bucket AWS dans lequel je veux sauvegarder mes fichiers

mon_bucket = "monprojet4"

# Methode de chargement d'un fichier dans le bucket par son nom
s3_resource.Bucket(mon_bucket).upload_file(Filename="/home/adminsys/mes_fichiers/fichier_test.txt"\
,Key="fichier_test.txt")

# Vérification de la sauvegarde

print("fichier sauvegardé sur s3 avec succès")

# Affichage du contenu du bucket

conn = boto3.client('s3')

# Levée d'une exception en cas d'erreur de frappe

# Utilisation de la boucle While
while True:

# Capture de la variable affichage
	affichage = input("Voulez vous afficher le contenu actuel de votre bucket?(o/n) :")
# Bloc try combiné d'une erreur d'assertion que je vais moi même créer
	try:
# Demande de vérification de la lettre tapée
		assert affichage == "o" or affichage=="n"
# Ce que l'on demande d'afficher en cas de non respect de la lettre demandée
	except AssertionError:
		print("Veuillez entrer o ou n :")
# Mot clé permettant de retourner au while afin de reposer la question
		continue
# Sinon si l'utilisateur tape o on demande l'affichage du contenu du bucket gràce a la boucle for
	else:
		if affichage == "o":
# qui va parcourir chaque élèment,l'inclure dans une variable nommée fichier et l'afficher
			for fichiers in conn.list_objects(Bucket=mon_bucket)['Contents']:
				print(fichiers['Key'])
# Demande d'arrêt de la boucle avec le mot-clé "break"
			break
# Sinon l'utilisateur a tapé "n" et l'on affiche "fin du traitement"
		else:
			print("fin du traitement")
			break

f = open("date_execution.txt","a")

f.write(f"Fcihier sauvegardé le : {datetime.now()}\n")

f.close()
