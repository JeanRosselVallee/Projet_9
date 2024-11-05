# Réalisez un traitement dans un environnement Big Data sur le Cloud
### But :
- Le but principal du traitement est la réduction de dimensions.
  - on a appliqué l'apprentissage par transfert au modèle pré-entraîné neuronal MobileNetV2

- Le jeu en entrée subit 2 réductions :
  - de 150 mille attributs on passe à un millier grâce à l'application d'un modèle neuronal
  - d'un millier on passe à une dizaine avec la réduction par PCA (analyse de composantes principales)

<img src="https://drive.google.com/file/d/1Ytgn1BWvweeD6pB6Ncdah64DLpJtIT5m/view?usp=drive_link" >

### Architecture
- l'utilisation du cluster chez Amazon facilite et simplifie le traitement et le transfert de données
  - Amazon EMR prend en charge une grande partie de la configuration du cluster
  - l'installation, la gestion et le traitement en arrière plan de Spark et de Hadoop se font de manière transparente pour le développeur
- Des clusters ont été créés par clonage. Ce qui est très rapide et simple.

#### Cluster EMR 
Les noeuds du cluster sont de 3 types
- Master
  - un serveur de notebooks JupyterHub qui tourne dans un conteneur Docker
  - le Driver Spark, qui distribue les tâches à éxecuter
  - généraliste moyennement puissant 
- Cores et Tasks
  - les Executors Spark réalisent le calcul de manière distribué 
  - le Core seul gère le stockage dans le système de fichiers de Hadoop HDFS
  - instances plus puissantes et spécifiques au calcul

#### Stockage S3
Il contient :
- le fichier avec la liste de modules Python à installer
- le notebook Jupyter
- les données et les résultats

#### Poste local
- on accède au noeud Master via un terminal SSH grâce à une paire de clés 
- pour éditer et lancer le traitement, notre navigateur se connecte au serveur de notebooks via un tunnel SSH et grâce à l'extension FoxyProxy

### Suivi du coût
- On a veillé à obtenir le prix le moins élevé des instances avec l'option Spot au lieu de l'option par défaut "On Demand"
- création de rapport de suivi hebdomadaire
- réception par mail de notifications SNS 
  - état change        -> “prêt”
  - fichier supprimé -> “fini”

### Jeu de données
- 10 mille images de fruits au format JPEG 
- regroupées dans 10 familles ou classes de fruits

### Outils : 
- AWS EMR, EC2 & S3
- PySpark
- TensorFlow
- JupyterHub
- FoxyProxy
- Bash
  
