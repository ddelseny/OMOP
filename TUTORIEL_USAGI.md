# TUTORIEL USAGI

En cours de développement...
## Téléchargement du vocabulaire sur Athena 
* Créer un compte sur le site Athena : 

[https://athena.ohdsi.org/auth/register](https://athena.ohdsi.org/auth/register)
* Dans la section Download (menu vert) : se loguer et sélectionner les vocabulaires de destination à télécharger. Ex : Loinc, RxNorm, Snomed, etc.

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
    +	source code column => codes
    +	source name column => libellé source en anglais
    +	source frequency column => nb de fois que ce libellé est observé dans la table
    +	Additional info column => libellé en français
    +	Laisser "Filter standard concepts" et "Include source domain" actifs
    +	Option 1 : Ajouter Filter by domain et choisir le domaine de destination 
      Ex : Drug, Measurment, Specimen, Spec disease status, Spec anatomic site, etc.
    + Option 2 : Ajouter Filter by vocabulary et choisir le vocabulaire de destination
      Ex : RxNorm, Loinc, etc.

![usagi16bio.png](images/usagi16bio.png)

NB : Si certaines colonnes ne sont pas visibles, utiliser l’ascenseur 

* Cliquer sur import 

Cela prend quelques minutes.

L’interface obtenue se divise en trois panneaux:
  * Vue de la table

![usagi19bio.png](images/usagi19bio.png)
 * Vue des mappings sélectionnés : liste un ou plusieurs **Target concepts** (une ou plusieurs lignes) possibles pour un même code source

![usagi20bio.png](images/usagi20bio.png)
  * Vue de la recherche
![usagi20bisbio.png](images/usagi20bisbio.png)
    + Pour rechercher un concept de destination : laisser Filter standard concepts et Include source terms  actifs et ajouter les filtres (filtrer sur le domaine/vocab choisi lors de l’import). Dans l’exemple ci-dessous les filtres sur le domaine **measurement** et le vocabulaire **Loinc** sont activés, nous obtenons plusieurs propositions :
![usagi21bio.png](images/usagi21bio.png)

    + L’option Query permet une recherche personnalisée
Avec l’option "Use source term" choisi par défaut, USAGI liste des propositions de mapping dans l’encart Results : sélectionner une des lignes proposées et cliquer sur « add concept» ou « replace concept » pour ajouter ou remplacer un concept dans la vue des mappings sélectionnés. **Il est possible d'avoir plusieurs concepts destinataires pour un même concept source**.
* Une fois les concepts de destination choisis dans la vue **Target concepts**, vous pouvez cliquer sur  ALT + C pour obtenir plus d'information sur le concept (hierarchie). 
* Tout en bas de la page, valider le mapping en cliquant sur **Approve** ou bien signaler ce mapping comme non approuvé en cliquant sur **Flag**.  
* L’utilisation des attributs EQUAL, EQUIVALENT, ETC. est optionnelle et ne sert qu’à commenter le fichier de travail (ces attributs n’apparaitront plus dans le fichier final exporté)

![usagi22bio.png](images/usagi22.png)

  + Une fois le mapping approuvé tous les **target concepts** sont associés au code source : la ligne dans la **vue de la table** est surlignée en vert et la ligne suivante est chargée.** De même si la ligne est signalée par un drapeau, la ligne est surlignée en rouge et la ligne suivante est chargée.

![usagi23bio.png](images/usagi23bio.png)

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
« Chu Bio » pour la bio
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
2.	Reconstruire l'index Usagi (Aide -> Reconstruire l'index).
3.	Ouvrer le fichier de mapping
4.	Identifier les codes qui correspondent à des concepts qui, dans la nouvelle version du vocabulaire, ne sont plus des concepts standard, et trouver des concepts cibles plus appropriés.






