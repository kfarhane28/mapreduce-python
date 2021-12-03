# MapReduce Python
## MapReduce Python Example

### Exemples : 
Vous êtes sensés faire que l'exemple 0 et l'exemple 1
	* Exemple 0: word count (vu en cours)
	* Exemple 1: Total des ventes par magasin
	* Exemple 4 (optionnel): Calculer maximum et minimum du salaire
	* Exemple 5 (optionnel): Calculer moyenne de l'écart type du Salaire
	* Exemple 6 (optionnel): Anagram 

### Exemple 0 : peu importe le format de fichier input: on veut compter le nombre d'occurrence de chaque mot dans le ou les fichiers input

### Exemple 1 : en à utiliser un fichier input sous la forme suivant:

		 date | temps | magasin| produit | cout | paiement

### Exemple 4 & 5: en à utiliser un fichier input sous la forme suivant:   

		 id , age , sexe , adresse , salaire

### Exemple 6 : en à utiliser un fichier input sous la forme suivant:

		melon barre deviner lemon
		arbre fiable fable vendre
		devenir faible barbe

### 1) comprendre le code python du mapper et reducer
ouvrir les ficher mapper.py et reducer.py pour l'exemple 0 et essayer de comprendre/comparer avec le cours.

### 2) Executer le program MapReduce Python on local (ceci est uniquement pour tester et valider le code Python du mapper et reducer)
pour test avant de passer en MapReduce pour détecter les erreurs Syntaxique
```bash
cat <chemin de fichier input on local> | python <chemin de fichier mapper.py on local> | python <chemin de fichier reducer.py on local>
```

### 3) Execution d'un exemple directement sur le cluster Hadoop (traitement parallèle distribué) :
on a choisi l'exemple 1 pour tester


```bash
# se mettre dans le repertoire local: /formation/mapreduce
cd /formation/mapreduce/exemple1
```

```bash
# créer répertoire input dans HDFS, ce répertoire va contenir le fichier de donnée input.txt
hdfs dfs -mkdir /user/<user>/input
```

```bash
# transférer le fichier input.text du local vers HDFS
hadoop fs -put input.txt  input/ 
```
```bash
# verifier que le fichier de donnée existe dans hdfs
hadoop fs -ls  input/ 
```

```bash
# execution Program Mapreduce
hadoop jar /usr/hdp/current/hadoop-mapreduce-historyserver/hadoop-streaming.jar \
-Dmaperd.reduce,tasks=1 \
-file /formation/mapreduce/exemple0/mapper.py \
-mapper "mapper.py" \
-file /formation/mapreduce/exemple0/reducer.py \
-reducer "reducer.py" \
-input input/input.txt \
-output out 
```
# 4) Vous pouvez verifier dans YARN UI ou Job History UI que le traitement MapReduce est terminé avec succès

```bash
# afficher le contenu de fichier output
hdfs dfs -cat out/part-00000 
```
# 5) nettoyer le repertoire out pour commencer avec l'exemple suivant:
```bash
# une fois terminé, supprimer du répertoire Output pour repartir avec l'exemple suivant (sinon utiliser un autre repertoire output)
hdfs dfs -rm -r out
```
