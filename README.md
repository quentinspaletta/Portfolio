Bonjour,

Bienvenue sur mon Portfolio.

Vous trouverez dans cet espace les projets que j'ai réalisé autour de l'analyse de données avec différents outils.

Projet 1 : Nettoyage de données en SQL

Projet 2 : Aller de la donnée brute à des visualitions claires et representatives de celle-ci avec Excel et Power BI

Les données brutes que j'ai utilisé sont repertoriées ici au format CSV.

Projet 1 :
D'abord un projet de "nettoyage" de données avec SQL en plusieurs étapes

1. Enlever les doublons
2. Uniformiser la donnée
3. Traiter les données manquantes
4. Enlever les données impertinentes

La donnée : 

<img width="802" height="259" alt="image" src="https://github.com/user-attachments/assets/bb399709-e13d-44f2-af71-e3dcc6d7bba1" />

J'ai travaillé sur un recensement des licenciements de différentes entreprise (company) dans différents secteurs (industry).
On peut deja constater que la données comporte des manquements dont je m'occuperai plus tard.

Vous trouverez le code de mes requêtes dans le document nommé "1.DATA CLEANNING PROJECT.sql"

1. Enlever les doublons

Pour les doublons, j'utilise la fonction row_number pour numéroter toutes les lignes en fonction de la majorité des colonnes.
Chaque ligne unique aura donc le numéro 1 et tout doublons incrementera ce numéro.

<img width="883" height="249" alt="image" src="https://github.com/user-attachments/assets/6569b283-6b0a-4766-9d76-0b211bf03420" />

Ensuite je créé la table comportant les numéros de ligne et je recupère dans celle ci les lignes avec un numéro supérieur à 1 pour voir les doublons.

<img width="890" height="111" alt="image" src="https://github.com/user-attachments/assets/3f42b164-c986-46ba-9124-85faf2418129" />


Je duplique la table initiale pour garder une sauvegarde de la table avant que je ne retire des données de celle ci puis je retire de ma duplication les doublons identifiés.


2.Uniformiser la donnée

Commençons par la colonne 'company' je commence par utiliser la fonction TRIM qui retire les potentiels espaces avant et après la donnée
Puis je regarde les différents secteurs 'industry' en utilisant un select DISTINCT.

<img width="114" height="347" alt="image" src="https://github.com/user-attachments/assets/262342a4-5511-4f83-ac86-db6e8024ff51" />

Je remarque que certaines entreprises n'ont pas eu de secteur attribué et que certains secteur sont similaires notamment sur la Crypto.

Je met alors à jour ma donnée, toujours sur la table dupliquée, et je transforme tout ce qui commence par 'Crypto...' par 'Crypto'
Pour mes données manquantes je remarque qu'il y a des valeurs NULL et des valeurs blanches, j'uniformise en Null

Une fois fait je verifie la mise à jour :

<img width="111" height="337" alt="image" src="https://github.com/user-attachments/assets/a0433505-bd69-4b30-9505-be31c2d9bc14" />

Ensuite en regardant la colonne des pays avec un Select distinct, je remarque une coquille dans la donnée.

<img width="147" height="339" alt="image" src="https://github.com/user-attachments/assets/a9c9c8a0-59e5-45c2-b3c4-33589bb5b6d6" />

Avec la fonction `trim(trailing '.' from country)` je met a jour ce défaut.

Passons a la colonne 'date', c'est la colonne qui m'a posé le plus de problèmes.

Déjà je remarque que ma colonne date est de type textuel et que le nom de ma colonne est un objet SQL (DATE)

Donc je dois changer ma date dans le format adéquat. J'utilise alors la fonction str_to_date sur ma date Pour ne pas citer l'objet et j'indique son format.

La date 1/18/2023 devient alors	2023-01-18

Je modifie le type de ma colonne : 

	alter table layoffs_staging2
	modify column `date` DATE;

Ma donnée est uniformisée !


Je m'occupe des Null :

Je fais donc une selection distincte sur chacune de mes colonnes pour repérer mes colonnes comportant des valeurs null

Comme vu précedement la colonne 'industry' en contient, je les affiche

<img width="873" height="121" alt="image" src="https://github.com/user-attachments/assets/8ba66403-1ae6-434a-9230-6c4ece49c300" />

`Select t1.location,t1.company,t1.industry, t2.location, t2.company, t2.industry

	from layoffs_staging2 t1
	join layoffs_staging2 t2
		On t1.company = t2.company
    	and t1.location = t2.location
	where (t1.industry is null)
	and t2.industry is not null;`

Dans cete requête je recupère ma table jointe avec elle même, où deux même entreprises d'un même endroit ont un secteur null et un secteur connu.

<img width="502" height="122" alt="image" src="https://github.com/user-attachments/assets/e718b23d-2520-49c5-85f9-da4f9b71abd0" />


Je remarque avoir des secteur non renseignées que je peut déduire. Le Airbnb de San Francisco est certainement dans le secteur du voyage comme son homologue.

Je met alors à jour ces informations.

Il y a aussi plusieurs manquements de valeurs dans les colonnes liées aux licenciements.

Puisque ce sont des valeur qui nous serviront pour notre analyse je décide de retirer toutes les lignes n'ayant aucune données dans le total de licenciements et le pourcentage du personnel licenciés.

Je commence par une requête SELECT pour m'assurer de ce que je vais retirer avant de le faire

	select *
	from layoffs
	where total_laid_off is null
	and percentage_laid_off is null;


<img width="831" height="264" alt="image" src="https://github.com/user-attachments/assets/ae3ee8a1-1061-402a-a5ce-53b1dc06ea06" />
<img width="971" height="12" alt="image" src="https://github.com/user-attachments/assets/af33acf7-ced7-4236-a38e-04b65c2f80ac" />

Je remarque que 362 lignes étaient impertinentes pour mes futures analyses, je les supprime. Me voilà soulagé.

Enfin je supprime la colonne de numérotage créée précédement.

Mes quatres étapes sont terminées j'ai maintenant des données prêtes à l'analyse.

Ce premier projet est complet et a developpé mes connaissances sur les principes complexes de SQL.
Je suis fier de ce travail.

Projet 2 : Un deuxième projet plus complet ou je vais utiliser les outils Excel et Power BI

La donnée represente les ventes d'une boutique axée jeux vidéos. Chaque ligne represente une commande comportant : ID, date d'achat, date de livraison, nom du produit, prix, plateforme d'achat, canal marketing et pays.
Des ventes étendues sur plus de 2 ans de janvier 2019 à mars 2021 soit prés de 22 000 commandes uniques

Je commence par explorer la donnée et regarder les potentielles erreurs ou incohérences qu'elle contient et je les note dans une feuille dédié

<img width="1317" height="229" alt="image" src="https://github.com/user-attachments/assets/ab7827a1-a4cd-4811-8d2f-05fa081282b8" />

J'ai donc uniformiser les nom des produits et les dates avec des fonctions SI et DATE, JOUR, MOIS, ANNEE 
Pour les region, j'ai utiliser la fonction RECHERCHEX pour recuperer la region associé au pays
Pour les doublons j'ai simplement utiliser un tableau croisé dynamique

Une fois la donnée propre, j'ai commencé à faire un premier tableau croisé dynamique avec une mise en forme conditionnelle pour commencer mon analyse.

<img width="1450" height="597" alt="image" src="https://github.com/user-attachments/assets/39e97be3-fcd9-498e-ae66-5a59a8a0cb65" />

Je tire de ce tableau mes premiers apercus

<img width="1547" height="155" alt="image" src="https://github.com/user-attachments/assets/6e1b6711-832e-40a0-a39b-0805c84f8367" />

Effectivement on remarque que certains produits sont plus performants que d'autres et que certains moment de l'année (Rentrée des classe, Noël) sont particulièrement performants aussi.

Voyons ca de plus près avec Power BI :

<img width="1301" height="652" alt="image" src="https://github.com/user-attachments/assets/c4c6d72b-06bf-4c0c-9b21-f536db6615b0" />

Si on regarde le nombre de commande au fil du temps, on se rend bien compte de la domination des mois de septembre et decembre.

On remarque aussi un nette amélioration des ventes entre 2019 et 2020.

Le produit "Playstation 5" est le facteur principale de cette fulgurance avec un nombre de commande et un revenue total multiplié par 5 entre janvier 2020 et mars 2020

<img width="831" height="376" alt="image" src="https://github.com/user-attachments/assets/a6d83947-98ba-4779-932d-41bff65acc6a" />

Il serait bon de regarder plus en profondeur avec l'èquipe marketing pour avoir le detail des promotions ou publicités faites pendant cette période.

La gamme des periphériques ne fonctionnent pas du tout en témoigne ce graphique représentant la part de chaque produit sur le revenue total :

<img width="853" height="633" alt="image" src="https://github.com/user-attachments/assets/44cd6283-c4de-4151-9ea7-b6739a18e2db" />

On peut se demander ce qui justifie ces resultats. Il faut revoir les produits en eux même ou la communication et le marketing autour.

En conclusion il pourrait être interessant d'appuyé la publicité et les efforts marketing autours des mois de septembre et décembre et agir sur les produits qui ne sont pas assez performants en changeant la méthode marketing ou en modifiant le produit.

On peut aussi pousser cette analyse en utilisant les dimensions démographiques comme les pays ou region pour plus de précision.

Pour finir un apercu du tableau de bord final :

<img width="1315" height="736" alt="image" src="https://github.com/user-attachments/assets/4e91d4e3-d3f1-4c95-a8f1-abf5540afc72" />


