=============
DEVELOPPEMENT
=============

Cette rubrique est destinée aux développeurs qui souhaiteraient...


Routes Symfony
--------------

Pour avoir toutes les routes à jour, il suffit dans symfony de lancer la commande
::

    php app/console router:debug

Aujourd'hui les différentes routes générées par symfony sont

Taxref
======

* /taxref/[?[limit=nb]&[page=nb]&[nom_valide=true]&[nomColonne=ValeurFiltre]*&[ilike=debutChaine]]
    * Remonte toutes les données de la table taxonomie.taxref
    * Méthode autorisée : GET
    * Paramètres autorisés : 
        * limit (defaut = 50) : nombre d'élément à retourner
        * page (defaut = 0) : page à retourner
        * nom_valide : ne retourne que les nom valides (cd_nom = cd_ref)
        * [nomColonne=ValeurFiltre]* = Permet de filtrer les données sur un ou plusieurs critères. Le nom du paramètre (nom_colonne) doit correspondre a un nom de champs de la table taxref au format camel case.
        * [ilike=debutChaine] = Ne revoie les données de la colonne lbNom qui commence par debutChaine
        
* /taxref/{id}
    * Remonte un enregistrement de la table taxonomie.taxref
    * Méthode autorisée : GET
    * Paramètre: l'id de l'enregistrement correspond au cd_nom du taxref
    
* /taxref/distinct/{field}[?[nomColonne=ValeurFiltre]*&[ilike=debutChaine]]
    * Remonte un distinct de la table taxonomie.taxref sur un champ spécifié
    * Méthode autorisée : GET
    * Paramètre obligatoire : le champ du distinct (n'importe quel champ de la table taxref)
    * Paramètres facultatifs : 
        * [nomColonne=ValeurFiltre]* = Permet de filtrer les données sur un ou plusieurs critères. Le nom du paramètre (nom_colonne) doit correspondre a un nom de champs de la table taxref au format camel case.
        * [ilike=debutChaine] = Ne revoie les données de la colonne recherchée qui commence par debutChaine
    * Exemples
        - /taxref/distinct/phylum : remonte tous les phylum de la table
        - /taxref/distinct/famille?regne=Plantae&ordre=Rosales : remonte les familles du regne Plantae et de l'ordre Rosales
        
* /taxref/hierarchie/{rang}[?[limit=nb]&[nomColonne=ValeurFiltre]*&[ilike=debutChaine]]
    * Selection des niveaux hiérarchiques de taxref avec le nombre de taxons associés aux différents rangs
    * Méthode autorisée : GET
    * Paramètre obligatoire : le nom du rang désiré
    * Paramètres facultatifs : 
        * limit (defaut = 10) : nombre d'élément à retourner
        * [nomColonne=ValeurFiltre]* = Permet de filtrer les données sur un ou plusieurs critères. Le nom du paramètre (nom_colonne) doit correspondre a un nom de champs de la table taxref au format camel case.
        * [ilike=debutChaine] = Ne revoie les taxons du rang recherché qui commence par debutChaine
    * Exemples
        - /hierarchie/FM?ordre=Chiroptera&limit=1000&regne=Animalia&ilike=m : remonte la liste des familles des chiroptères qui commencent par un m

Bibtaxons
=========

* /bibtaxons/ 
    * Remonte toutes les données de la table taxonomie.bib_taxons
    * Méthode autorisée : GET
    
* /bibtaxons/taxonomie
    * Remonte cd_nom, cd_taxsup, lb_nom et id_rang pour les familles, ordre, classe, phylum et regne des enregistrements de la table taxonomie.bibtaxons
    * Méthode autorisée : GET
    
* /bibtaxons/{id}
    * Remonte un enregistrement de la table taxonomie.bib_taxons
    * Méthode autorisée : GET
    * Paramètre: l'id de l'enregistrement
    
* /bibtaxons/{id} 
    * Création ou mise à jour d'un enregistrement dans la table taxonomie.bib_taxons
    * Méthode autorisée : POST|PUT
    * Paramètre: l'id de l'enregistrement (si update) ou rien (si create)
    
* /bibtaxons/{id} 
    * SUppression d'un enregistrement dans la table taxonomie.bib_taxons
    * Méthode autorisée : DELETE
    * Paramètre: l'id de l'enregistrement à supprimer
    
Biblistes
=========
* /biblistes/[{id}]
    * Selection des données relatives à la ou aux listes avec les taxons associés
    * Méthode autorisée : GET
    * Paramètres facultatifs : 
        * id : identifiant de la liste
        
* /biblistes/simpleliste
    * Selection des données contenues uniquement dans la table biblistes
    * Méthode autorisée : GET
    
* /biblistes/taxonliste/{id}
    * Selection des taxons associés à la liste demandée
    * Méthode autorisée : GET
    * Paramètre obligatoire : 
        * id : identifiant de la liste

Bibfiltres
==========
* /bibfiltres/
    * Remonte toutes les données de la table taxonomie.bib_filtres
    * Méthode autorisée : GET
    
* /bibfiltres/{id}
    * Remonte un enregistrement de la table taxonomie.bib_filtres
    * Méthode autorisée : GET
    * Paramètre: l'id de l'enregistrement


Bla bla bla
-----------

The most minimal components required to run an instance are :

* PostGIS 2 server
* GDAL, GEOS, libproj
* gettext
* libfreetype
* libxml2, libxslt
* Usual Python dev stuff

A voir : `the list of minimal packages on Debian/Ubuntu <https://github.com/makinacorpus/Geotrek/blob/211cd/install.sh#L136-L148>`_.

.. note::

    En lancant ``env_dev`` et ``update`` is recommended after a pull of new source code,
    but is not mandatory : ``make serve`` is enough most of the time.
