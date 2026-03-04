Bonjour,
Bienvenue sur mon Portfolio.
Vous trouverez dans cet espace les projets que j'ai réalisé autour de l'analyse de données avec différents outils.

D'abord un projet de "nettoyage" de données avec SQL en plusieurs étapes

1. Enlever les doublons
2. Uniformiser la donnée
3. Traiter les données manquantes
4. Enlever les données impertinentes

Pour les doublons, j'utilise la fonction row_number pour numéroter toutes les lignes en fonction de la majorité des colonnes.
Chaque ligne unique aura donc le numéro 1 et tout doublons incrementera ce numéro.

<img width="883" height="249" alt="image" src="https://github.com/user-attachments/assets/6569b283-6b0a-4766-9d76-0b211bf03420" />

Ensuite je créé la table comportant les numéros de ligne et je recupère dans celle ci les lignes avec un numéro supérieur à 1 pour voir les doublons.
Je duplique la table initiale pour garder une sauvegarde de la table avant que je ne retire des données de celle ci puis je retire de ma duplication les doublons identifiés.



Ce premier projet est complet et a developpé mes connaissances sur les principes complexes de SQL comme les Subqueries, CTEs et Window functions.
