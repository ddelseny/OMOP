# TUTORIEL USAGI

En cours de développement...
## Téléchargement du vocabulaire sur Athena 
* Créer un compte sur le site Athena : 

[https://athena.ohdsi.org/auth/register](https://athena.ohdsi.org/auth/register)
* Dans la section Download (menu vert) : se loguer et sélectionner les vocabulaires de destination à télécharger. Ex : Loinc, Specimen type, Snomed, etc.

![athenaInterface.png](images/athenaInterface.PNG)
* Cliquer sur Download vocabularies
![athenaDownloadSummary.png](images/athenaDownloadSummary.PNG)
* Nommer le fichier et s'assurer que la version du CDM est 5.x
* Sélectionner ou non la case de notification pour être informé par email de mises à jour des vocabulaires sélectionnés puis cliquer sur Download.

![summary2.png](images/summary3.png)
* Un lien pour télécharger le fichier *.zip contenant le vocabulaire vous est envoyé par email
* Copier et dé-zipper ce fichier sous le chemin de votre choix. Ex : C:\Athena

![vocab4.png](images/vocab4.png)
## Installation de Usagi
* Pré requis : java 1.8 ou plus
* Dans la section Assets de la page [https://github.com/OHDSI/Usagi/releases](https://github.com/OHDSI/Usagi/releases)
![usagi5.png](images/usagi5.png)
* Télécharger Usagi_v*.jar et copier ce fichier sous le chemin de votre choix dans un répertoire que vous devez créer, nommé Usagi. Exemple de chemin : C:\Usagi
* Entrer votre nom et cliquer sur remember me

![usagi6.png](images/usagi6.png)
## Import du vocabulaire sur USAGI
* Cliquer sur Help >> Rebuild index

![usagi7.png](images/usagi7.png)
* Cliquer sur Pick folder et sélectionner le chemin vers les vocabulaires importés 

![usagi8.png](images/usagi8.png)
*	Utiliser la flèche pour remonter dans l’arborescence
*	Cliquer sur Select folder puis sur Build index

![usagi9.png](images/usagi9.png)

![usagi10.png](images/usagi10.png)

La construction de l’index prend plusieurs minutes…

![usagi11.png](images/usagi11.png)
* Une fois l’index construit, relancer Usagi.

![usagi12.png](images/usagi12.png)

## Préparation des données à mapper
Le fichier importé doit comporter au moins les colonnes contenant le code source et une description du code source en anglais, mais des informations supplémentaires sur les codes peuvent également être importées (par exemple, l'unité de dose, la description en français, la fréquence des codes). 
* Dans un fichier Excel, organiser les données de la façon suivante :
  + Une colonne pour les codes 
  + Une colonne pour les libellés en français que l’on cherche à mapper
  + Une colonne pour la traduction de ces libellés (utiliser deepl ou google translate)
  + Une colonne pour les fréquences

Exemple de fichier Excel pour l'import :

![usagi13.png](images/usagi13.png)

## Importer le fichier sous USAGI

* Depuis le menu File, cliquer sur import codes

![usagi14.png](images/usagi14.png)
* Ouvrir le fichier Excel qui contient les données 

![usagi15.png](images/usagi15.png)
*	Dans la section Column mapping (en bas à gauche), faire correspondre les colonnes du fichier Excel avec celles attendues : 
    +	source name column => libellé source en anglais
    +	source frequency column => nb de fois que ce libellé est observé dans la table
    +	Additional info column => libellé en français
    +	Laisser "Filter standard concepts" et "Include source domain" actifs
    +	Option 1 : Ajouter Filter by domain et choisir le domaine de destination 
      Ex : Specimen, Spec disease status, Spec anatomic site, etc.
    + Option 2 : Ajouter Filter by vocabulary et choisir le vocabulaire de destination
      Ex : Loinc

![usagi16.png](images/usagi16.png)

NB : Si certaines colonnes ne sont pas visibles, utiliser l’ascenseur 

![usagi17.png](images/usagi17.png)

* Cliquer sur import 

![usagi18.png](images/usagi18.png)

Cela prend quelques minutes.

* L’interface obtenue se divise en trois panneaux:
  + Vue de la table

![usagi19.png](images/usagi19.png)
  + Vue des mappings sélectionnés 

![usagi20.png](images/usagi20.png)
  + Vue de la recherche

![usagi20bis.png](images/usagi20bis.png)
  - Laisser Filter standard concepts et Include source terms  actifs
   
  - Ajouter filter by domain (filtrer sur le domaine choisi lors de l’import) 

Dans l’exemple ci-dessous si le filtre sur le domaine spec disease status est activé, nous obtenons trois propositions :
![usagi21.png](images/usagi21.png)

  - L’option Query permet une recherche personnalisée
  - Avec l’option Use source term choisi par défaut, USAGI liste des propositions de mapping dans l’encart Results.
  - Sélectionner une des lignes proposées et cliquer sur « add concept» ou « replace concept » pour ajouter ou remplacer un concept dans la vue des mappings sélectionnés. *Il est possible d'avoir plusieurs concepts destinataires pour un même concept source*.
  - Il est possible de mettre un drapeau ou d’approuver directement la proposition de mapping. 
  - L’utilisation des attributs EQUAL, EQUIVALENT, ETC. est optionnelle et ne sert qu’à commenter le fichier de travail (ces attributs n’apparaitront plus dans le fichier final exporté)
![usagi22.png](images/usagi22.png)

* Une fois approuvée ou signalée par un drapeau, *tous les mappings de la vue des mappings sélectionnés* sont associés au code source et la ligne suivante est chargée.

Après signalement par un drapeau, les lignes dans la vue de la table sont écrites en rouge. Après approbation, elles sont surlignées en vert :
![usagi23.png](images/usagi23.png)

* Si aucune proposition ne convient : signaler la ligne par un drapeau => ne pas approuver, ajouter UNMATCHED si besoin (ou autres options utiles pour ce fichier de travail)

![usagi24.png](images/usagi24.png)

NB : Penser à changer l’attribut sur la prochaine ligne 
*	Il est possible de sauver ce document de travail afin d’y revenir plus tard 

![usagi25.png](images/usagi25.png)

## Reprendre un mapping en cours

* Relancer USAGI (fichier jar)
* Cliquer sur File >> Open

![usagi26.png](images/usagi26.png)

* Continuer le mapping : seules les lignes approuvées seront exportées 

NB :  si pour un libellé source, il n’existe pas de correspondance, la ligne est signalée par un drapeau, elle ne sera pas exportée.

## Export des résultats

* Dans le menu File, cliquer sur Export source to concept map

![usagi29.png](images/usagi29.png)

ATTENTION IMPORTANT : choisir "Only approved" pour n’exporter que le mapping approuvé

Export for review

![usagi30.png](images/usagi30.png)

*	Choisir un id pour le vocabulaire :
L’id doit être court et peut comporter des espaces
 ex : 
« Chu Spec » pour le domaine specimen
« Chu Spec Anat » pour le domaine spec anatomic site
« Chu Spec Disease » pour le domaine spec disease status

![usagi31.png](images/usagi31.png)
* Nommer le fichier résultat en précisant le domaine cible :
Ex : MPTL_CHU_SPEC_DISEASE pour le domaine spec disease status

![usagi32.png](images/usagi32.png)


-------------------------- SECTION EN COURS DE DEV--------------------------
##	Mise à jour du vocabulaire
1.	Télécharger les nouveaux fichiers de vocabulaire depuis Athena
2.	Reconstruiser l'index Usagi (Aide -> Reconstruire l'index).
3.	Ouvrer le fichier de mapping
4.	Identifier les codes qui correspondent à des concepts qui, dans la nouvelle version du vocabulaire, ne sont plus des concepts standard, et trouver des concepts cibles plus appropriés.






