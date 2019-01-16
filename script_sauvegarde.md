#!/usr/bin/env python3.6

# importation de la librairie boto3

import boto3

# Renseignement du service AWS auquel je souhaiterais accéder
s3_resource = boto3.resource('s3')

# Renseignement des clés d'accès afin de se connecter automatiquement au compte AWS
ACCES_KEY_ID = "AKIAJD77J7MUBAVEACZQ"

ACCESS_SECRET_KEY = "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"

# Renseignement du nom du bucket AWS dans lequel je veux sauvegarder mes fichiers
mon_bucket = "monprojet4"

# Methode de chargement d'un fichier dans le bucket par son nom
s3_resource.Bucket(mon_bucket).upload_file(Filename="/home/adminsys/mes_fichiers/fichier_test.txt",Key="fichier_test.txt")

# Affichage du contenu du bucket
print("fichier sauvegardé sur s3 avec succès")

affichage=input("Voulez vous afficher le contenu actuel de votre bucket?(o/n)")

conn = boto3.client('s3')

try:
	affichage = str(affichage)
	if affichage != "o" or "n"
		raise ValueError("Veuillez entre o ou n")
if affichage == "o":
	for fichiers in conn.list_objects(Bucket=mon_bucket)['Contents']:
		print(fichiers['Key'])
else:
	print("fin du traitement")
