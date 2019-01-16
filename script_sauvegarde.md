#!/usr/bin/env python3.6

# importation de la librairie boto3

import boto3
import botocore

# Renseignement du service AWS auquel je souhaiterais accéder
s3_resource = boto3.resource('s3')
# Renseignement des clés d'accès afin de se connecter automatiquement au compte AWS
ACCES_KEY_ID = "AKIAJD77J7MUBAVEACZQ"
ACCESS_SECRET_KEY = "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"

# Renseignement du nom du bucket AWS dans lequel je veux sauvegarder mes fichiers
BUCKET_NAME = "monprojet4"

# Methode de chargement d'un fichier dans le bucket par son nom
s3_resource.Bucket(BUCKET_NAME).upload_file(Filename="/home/adminsys/mes_fichiers/fichier_test.txt",Key="fichier_test.txt")

# Affichage
print("fichier sauvegardé sur s3 avec succes")

affichage=input("Voulez vous afficher le contenu actuel de votre bucket?")

conn = boto3.client('s3')

if affichage == "oui":
	for fichiers in conn.list_objects(Bucket=BUCKET_NAME)['Contents']:
		print(fichiers['Key'])
else:
	print("fin du traitement")
