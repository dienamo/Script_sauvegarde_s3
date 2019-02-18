#!/usr/bin/env python3.6

# importation de la librairie boto3
import boto3

# Importation du module datetime pour inscrire la date et l'heure d'éxècution du script
from datetime import datetime
import time

# On declare le service AWS auquel on souhaiterais accéder
s3_resource = boto3.resource('s3')

# On déclare le nom du bucket AWS dans lequel on veut sauvegarder les fichiers
mon_bucket="monprojet4"

# On determine le moment du début de l'execution de la savegarde
début = time.time()

# Methode de chargement d'un fichier dans le bucket par son nom
s3_resource.Bucket(mon_bucket).upload_file(Filename="lignes"\
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

