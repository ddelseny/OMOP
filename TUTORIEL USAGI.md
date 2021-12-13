# TUTORIEL USAGI

En cours de développement...
## Téléchargement du vocabulaire sur Athena 
* Créer un compte sur le site Athena : [https://athena.ohdsi.org/auth/register](https://athena.ohdsi.org/auth/register)
* Dans la section Download (menu vert) : se loguer et sélectionner les vocabulaires de destination à télécharger. Ex : Loinc, Specimen type, Snomed, etc.
![athenaInterface.png](athenaInterface.png)
* Cliquer sur Download vocabularies
![athenaDownloadSummary.png](athenaDownloadSummary.png)
* Nommer le fichier et s'assurer que la version du CDM est 5.x
* Sélectionner ou non la case de notification pour être informé par email de mises à jour des vocabulaires sélectionnés puis cliquer sur Download.
![summary2.png](summary3.png)
* Un lien pour télécharger le fichier *.zip contenant le vocabulaire vous est envoyé par email
* Copier et dé-zipper ce fichier sous le chemin de votre choix. Ex : C:\Athena
![vocab4.png](vocab4.png)
## Installation de Usagi
* Pré requis : java 1.8 ou plus
* Dans la section Assets de la page [https://github.com/OHDSI/Usagi/releases](https://github.com/OHDSI/Usagi/releases)
* Télécharger Usagi_v*.jar et copier ce fichier sous le chemin de votre choix dans un répertoire que vous devez créer, nommé Usagi. Exemple de chemin : C:\Usagi
* Entrer votre nom et cliquer sur remember me
![usagi6.png](usagi6.png)
## Import du vocabulaire sur USAGI
* Cliquer sur Help >> Rebuild index
![usagi7.png](usagi7.png)
* Cliquer sur Pick folder et sélectionner le chemin vers les vocabulaires importés 
![usagi8.png](usagi8.png)
*	Utiliser la flèche pour remonter dans l’arborescence
*	Cliquer sur Select folder puis sur Build index
![usagi9.png](usagi9.png)
* Cliquer sur Select folder et cliquez sur Build index 
![usagi10.png](usagi10.png)
La construction de l’index prend plusieurs minutes…
![usagi11.png](usagi11.png)
* Une fois l’index construit, relancer Usagi.
* ![usagi12.png](usagi12.png)
## Préparation des données à mapper
* Dans un fichier Excel, organiser les données de la façon suivante :
- Une colonne pour les codes (si présents)
-	Une colonne pour les libellés en français que l’on cherche à mapper
-	Une colonne pour la traduction de ces libellés (utiliser deepl ou google translate)
-	Une colonne pour les fréquences

