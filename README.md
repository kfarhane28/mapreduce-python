# MapReduce Python
## MapReduce Python Example

### Exemples : 

	* Exemple 0: word count vu en cours
	* Exemple 1: Total des ventes par magasin
	* Exemple 4: Calculer maximum et minimum du salaire
	* Exemple 5: Calculer moyenne de l'écart type du Salaire
	* Exemple 6: Anagram 

### Exemple 0 : peu importe le format de fichier input:

### Exemple 1 : en à utiliser un fichier input sous la forme suivant:

		 date | temps | magasin| produit | cout | paiement

### Exemple 4 & 5: en à utiliser un fichier input sous la forme suivant:   

		 id , age , sexe , adresse , salaire

### Exemple 6 : en à utiliser un fichier input sous la forme suivant:

		melon barre deviner lemon
		arbre fiable fable vendre
		devenir faible barbe

### Executer le program MapReduce Python on local
pour test avant de passer en MapReduce pour détecter les erreurs Syntaxique
```bash
cat <chemin de fichier input on local> | python <chemin de fichier mapper.py on local> | python <chemin de fichier reducer.py on local>
```
### Copier le fichier input on HDFS
```bash
hdfs dfs -put <chemin du ficher input on Local> <nom de dossier de destination>
```
ou : 
```bash
hadoop fs -put <chemin du fichier input on Local> <nom de dossier de destination>
```
### Commande d'exécution du program MapReduce en Python :

```bash
hadoop jar <chemin de fichier streaming.jar> 
-Dmaperd.reduce,tasks=1
-file  <chemin du ficher map on Local>
-mapper "mapper.py"
-file <chemin du ficher reduce on Local>
-reducer "reducer.py"
-input <chemin du ficher input on HDFS>
-output <chemin du ficher output on HDFS>
```

### Commande d'afficher contenu de fichier Output :

```bash
hdfs dfs -cat <chemin de fichier output>/part-00000 
```

### Commande de suppression du répertoire Output :

```bash
hdfs dfs -rm -r <répertoire de fichier output>
```

### Execution d'un exemple :
en va choisi l'exemple 1 pour tester

copier l'exemple 1 dans le chemin suivant: /formation/mapreduce

```bash
# créer répertoire input dans HDFS
hdfs dfs -mkdir /user/<user>/input
```

```bash
# transférer le fichier input.text du local vers HDFS
hadoop fs -put /formation/mapreduce/example1/input.txt  input/ 
```

```bash
# execution Program Mapreduce
hadoop jar /usr/hdp/current/hadoop-mapreduce-historyserver/hadoop-streaming.jar
-Dmaperd.reduce,tasks=1
-file /formation/mapreduce/exemple1/mapper.py
-mapper "mapper.py"
-file /formation/mapreduce/example1/reducer.py
-reducer "reducer.py"
-input input/input.txt
-output out
```

```bash
# afficher le contenu de fichier output
hdfs dfs -cat out/part-00000 
```

```bash
# suppression du répertoire Output
hdfs dfs -rm -r out
``
