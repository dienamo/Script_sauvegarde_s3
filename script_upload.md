#!/usr/bin/env python3.6
import boto3
from datetime import datetime
import time
import os
import sys
s3_resource = boto3.resource('s3')
mon_bucket = "monprojet6"

from argparse import ArgumentParser
parser = ArgumentParser()
parser.add_argument("-f", action="store_true",dest="chemin",help="chemin de location restauration")
parser.add_argument("-b","--bucket",help="nom du bucket")
parser.add_argument("-c","--path",help="chemin de location restauration")
# On déclare la variable args qui représente la methode parse_args utilisée par Argumentparser
args = parser.parse_args()

mon_bucket = args.bucket

chemin = args.chemin
début = time.time()

# On determine le moment du début de l'execution de la sauvegarde
if args.chemin:

	f = open(os.path.join('/home/adminsys/fichier_aws.txt')).read().splitlines()

	for fichier in f:
		if os.path.exists(fichier):
			s3_resource.Bucket(mon_bucket).\
			upload_file(Filename = f'{fichier}',Key =os.path.basename(fichier))
			print("-----------------------------------------")
			print("Sauvegarde multiple effectuée avec succès")
			print("-----------------------------------------")

		else:
			print(f'fichier {os.path.basename(fichier)} introuvable dans {os.path.dirname(fichier)}')
			f = open("Fichiers_en erreur.txt","a")
			f.write(f'fichier {os.path.basename(fichier)} introuvable dans {os.path.dirname(fichier)}\n')
			f.close()
# Methode de chargement d'un fichier dans le bucket par son nom
# On determine le moment de la fin de la sauvegarde
	fin = time.time()

# On affiche un message indiquant la fin de la sauvegarde

#On affiche un message indiquant le temps de la sauvegarde
else:
	while True:

		fichier = input("Quel fichier voulez vous sauvegarder? ('q' pour quitter): ")

		try:
			assert fichier != 'q'

		except AssertionError:

			sys.exit()

		chemin = input("Veuillez entrer le chemin du fichier à sauvegarder :")


		if os.path.exists(fichier):
			s3_resource.Bucket(mon_bucket).upload_file(Filename = f'{chemin}{fichier}',Key = fichier)
			print("---------------------------------------")
			print("Sauvegarde unique effectuée avec succès")
			print("---------------------------------------")
			break
		else:
			print(f'fichier {os.path.basename(fichier)} introuvable dans {chemin}')
			continue
