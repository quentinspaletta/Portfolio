Bonjour,
Bienvenue sur mon Portfolio.
Vous trouverez dans cet espace les projets que j'ai réalisé autour de l'analyse de données avec différents outils.

D'abord un projet de "nettoyage" de données avec SQL en plusieurs étapes

1. Enlever les doublons
2. Uniformiser la donnée
3. Traiter les données manquantes
4. Enlever les données impertinentes

La donnée : 
<img width="802" height="259" alt="image" src="https://github.com/user-attachments/assets/bb399709-e13d-44f2-af71-e3dcc6d7bba1" />

J'ai travaillé sur un recensement des licenciements de différentes entreprise (company) dans différents secteurs (industry).
On peut deja constater que la données comporte des manquements dont on s'occupera plus tard.


1. Enlever les doublons
Pour les doublons, j'utilise la fonction row_number pour numéroter toutes les lignes en fonction de la majorité des colonnes.
Chaque ligne unique aura donc le numéro 1 et tout doublons incrementera ce numéro.

<img width="883" height="249" alt="image" src="https://github.com/user-attachments/assets/6569b283-6b0a-4766-9d76-0b211bf03420" />

Ensuite je créé la table comportant les numéros de ligne et je recupère dans celle ci les lignes avec un numéro supérieur à 1 pour voir les doublons.

<img width="890" height="111" alt="image" src="https://github.com/user-attachments/assets/3f42b164-c986-46ba-9124-85faf2418129" />


Je duplique la table initiale pour garder une sauvegarde de la table avant que je ne retire des données de celle ci puis je retire de ma duplication les doublons identifiés.


2.Uniformiser la donnée

On commence par la colonne 'company' je commence par utiliser la fonction TRIM qui retire les potentiels espaces avant et après la donnée
Puis je regarde les différents secteurs 'industry' en utilisant un select DISTINCT.

<img width="114" height="347" alt="image" src="https://github.com/user-attachments/assets/262342a4-5511-4f83-ac86-db6e8024ff51" />

On remarque que certaines entreprises n'ont pas eu de secteur attribué et que certains secteur sont similaires notamment sur la Crypto.
Je met alors à jour ma donnée, toujours sur la table dupliquée, et je transforme tout ce qui commence par 'Crypto...' par 'Crypto'
Pour mes données manquantes on remarque qu'il y a des valeurs NULL et des valeurs blanches, j'uniformise en Null
Une fois fait je verifie la mise à jour :

<img width="111" height="337" alt="image" src="https://github.com/user-attachments/assets/a0433505-bd69-4b30-9505-be31c2d9bc14" />

Ensuite en regardant la colonne des pays avec un Select distinct, je remarque une coquille dans la donnée.

<img width="147" height="339" alt="image" src="https://github.com/user-attachments/assets/a9c9c8a0-59e5-45c2-b3c4-33589bb5b6d6" />

Avec la fonction trim(trailing '.' from country) je met a jour ce défaut.



Ce premier projet est complet et a developpé mes connaissances sur les principes complexes de SQL comme les Subqueries, CTEs et Window functions.
