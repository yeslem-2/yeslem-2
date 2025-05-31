TP5 - Système d’Exploitation - Solutions

Exercice 1 - Vérification et création de fichier
1. Créer un script shell qui prend un nom de fichier en argument :
```bash
#!/bin/bash
if [ -z "$1" ]; then
  echo "Usage: $0 <nom_du_fichier>"
  exit 1
fi

if [ -e "$1" ]; then
  echo "Le fichier existe"
else
  touch "$1"
  echo "Le fichier a ete cree"
fi
```

2. Test du script :
```bash
./script.sh fichier_existant.txt
./script.sh fichier_inexistant.txt
```

Exercice 2 - Boucle for
1. Affichage des nombres de 1 à 10 :
```bash
#!/bin/bash
for i in {1..10}; do
  echo $i
done
```

2. Affichage des nombres pairs de 2 à 10 :
```bash
#!/bin/bash
for i in {2..10..2}; do
  echo $i
done
```

Exercice 3 - Compter lignes et mots
```bash
#!/bin/bash
FILE=$1

if [ -z "$FILE" ]; then
  echo "Veuillez fournir un fichier en parametre."
  exit 1
fi

if [ ! -f "$FILE" ]; then
  echo "Fichier non trouve."
  exit 2
fi

lignes=$(wc -l < "$FILE")
mots=$(wc -w < "$FILE")
echo "Nombre de lignes : $lignes"
echo "Nombre de mots : $mots"
```

Exercice 4 - Fonction sur deux nombres
```bash
#!/bin/bash

calculs() {
  a=$1
  b=$2

  echo "Somme: $((a + b))"
  echo "Difference: $((a - b))"
  echo "Produit: $((a * b))"
  echo "Quotient: $((a / b))"
  echo "Racine carrée de $a: $(echo "sqrt($a)" | bc -l)"
  echo "Racine carrée de $b: $(echo "sqrt($b)" | bc -l)"
}

calculs $1 $2
```

Exercice 5 - Fonction avec plusieurs arguments
```bash
#!/bin/bash

plus_grand() {
  max=$1
  for n in "$@"; do
    if (( n > max )); then
      max=$n
    fi
  done
  echo "Le plus grand est : $max"
}

plus_grand "$@"
echo "Paramètres passés : $@"
```

Exercice 6 - Script de sauvegarde
```bash
#!/bin/bash

DIR=$1
BACKUP_DIR=./backups
mkdir -p "$BACKUP_DIR"

DATE=$(date +%F)
ARCHIVE="$BACKUP_DIR/backup-$DATE.tar.gz"

tar -czf "$ARCHIVE" "$DIR"

# Supprimer les sauvegardes de plus de 7 jours
find "$BACKUP_DIR" -type f -name "backup-*.tar.gz" -mtime +7 -exec rm {} \;

echo "Sauvegarde créée : $ARCHIVE"
```
