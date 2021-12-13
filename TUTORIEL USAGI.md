# TUTORIEL USAGI

En cours de développement...
## Téléchargement du vocabulaire sur Athena 
* Créer un compte sur le site Athena : 

[https://athena.ohdsi.org/auth/register](https://athena.ohdsi.org/auth/register)
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
* Cliquer sur Select folder et cliquer sur Build index 

![usagi10.png](usagi10.png)
La construction de l’index prend plusieurs minutes…

![usagi11.png](usagi11.png)
* Une fois l’index construit, relancer Usagi.

![usagi12.png](usagi12.png)

## Préparation des données à mapper
* Dans un fichier Excel, organiser les données de la façon suivante :
  + Une colonne pour les codes (si présents)
  + Une colonne pour les libellés en français que l’on cherche à mapper
  + Une colonne pour la traduction de ces libellés (utiliser deepl ou google translate)
  + Une colonne pour les fréquences

Exemple de fichier Excel pour l'import :

![usagi13.png](usagi13.png)

## Importer le fichier sous USAGI

* Depuis le menu File, cliquer sur import codes

![usagi14.png](usagi14.png)
* Ouvrir le fichier Excel qui contient les données 

![usagi15.png](usagi15.png)
*	Dans la section Column mapping (en bas à gauche), faire correspondre les colonnes du fichier Excel avec celles attendues : 
  +	source name column => libellé source en anglais
  +	source frequency column => nb de fois que ce libellé est observé dans la table
  +	Additional info column => libellé en français
  +	Laisser Filter standard concepts, Include source domain actifs
  +	Ajouter Filter by domain et choisir le domaine de destination 
    -	Ex : Specimen, Spec disease status, Spec anatomic site, etc.

![usagi15.png](usagi15.png)
NB : Si certaines colonnes ne sont pas visibles, utiliser l’ascenseur 

![usagi16.png](usagi16.png)

* Cliquer sur import 

![usagi17.png](usagi17.png)

Cela prend quelques minutes.

* L’interface obtenue se divise en trois panneaux:
  + Vue de la table

![usagi18.png](usagi18.png)
  + Vue des mappings sélectionnés 

![usagi19.png](usagi19.png)
  + Vue de la recherche

![usagi20.png](usagi20.png)
    - Laisser Filter standard concepts et Include source terms  actifs
     - Ajouter filter by domain (filtrer sur le domaine choisi lors de l’import) 

Dans l’exemple ci-dessous si le filtre sur le domaine spec disease status est activé, nous obtenons trois propositions :
![usagi21.png](usagi21.png)

  - L’option Query permet une recherche personnalisée
  - Avec l’option Use source term choisi par défaut, USAGI liste des propositions de mapping dans l’encart Results.
  - Sélectionner une des lignes proposées et cliquer sur « add concept» ou « replace concept » pour ajouter ou remplacer un concept dans la vue des mappings sélectionnés. Il est possible de garder plusieurs concepts dans cette vue pour une révision future.
  - Il est possible de mettre un drapeau ou d’approuver directement une proposition de mapping. 
  - L’utilisation des attributs EQUAL, EQUIVALENT, ETC. est optionnelle et ne sert qu’à commenter le fichier de travail (ces attributs n’apparaitront plus dans le fichier final exporté)
![usagi22.png](usagi22.png)

* Une fois approuvée ou signalée par un drapeau, la proposition est mise à jour dans la vue de la table et la ligne suivante est chargée.

Après signalement par un drapeau, les lignes dans la vue de la table sont écrites en rouge. Après approbation, elles sont surlignées en vert :
![usagi23.png](usagi23.png)

* Si aucune proposition ne convient : signaler la ligne par un drapeau => ne pas approuver, ajouter UNMATCHED si besoin (ou autres options utiles pour ce fichier de travail)

![usagi24.png](usagi24.png)

NB : Penser à changer l’attribut sur la prochaine ligne 
*	Il est possible de sauver ce document de travail afin d’y revenir plus tard 

![usagi25.png](usagi25.png)

## Reprendre un mapping en cours

* Relancer USAGI (fichier jar)
* Cliquer sur File >> Open

![usagi26.png](usagi26.png)

* Continuer le mapping : seules les lignes approuvées seront exportées 
NB :  si pour un libellé source, il n’existe pas de correspondance, la ligne est signalée par un drapeau, elle ne sera pas exportée.

## Export des résultats

* Dans le menu File, cliquer sur Export source to concept map

![usagi27.png](usagi27.png)

ATTENTION IMPORTANT : choisir "Only approved" pour n’exporter que le mapping approuvé

Export for review

![usagi28.png](usagi28.png)

*	Choisir un id pour le vocabulaire :
L’id doit être court et peut comporter des espaces
 ex : 
« Chu Spec » pour le domaine specimen
« Chu Spec Anat » pour le domaine spec anatomic site
« Chu Spec Disease » pour le domaine spec disease status

![usagi29.png](usagi29.png)
* Nommer le fichier résultat en précisant le domaine cible :
Ex : MPTL_CHU_SPEC_DISEASE pour le domaine spec disease status

![usagi30.png](usagi30.png)


-------------------------- SECTION EN COURS DE DEV--------------------------
##	Mise à jour du vocabulaire
1.	Télécharger les nouveaux fichiers de vocabulaire depuis Athena
2.	Reconstruiser l'index Usagi (Aide -> Reconstruire l'index).
3.	Ouvrer le fichier de mapping
4.	Identifier les codes qui correspondent à des concepts qui, dans la nouvelle version du vocabulaire, ne sont plus des concepts standard, et trouver des concepts cibles plus appropriés.






