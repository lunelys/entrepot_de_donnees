# entrepot_de_donnees
Repositoire dans le cadre du cours entrepôt de données avec mon binôme Malo RIGOLAND, instructeur Franck AMANA

Résumé des TPs :

## Séance 1 : Introduction
Création d'une fiche KPIs :

| Nom | Intitulé | Table reliée | Comment calculer |
| --- | --- | --- | --- |
| chiffre_affaire | Chiffre d’affaire | orders | Montant total x nombre |
| sales_volume_per_product | Volume de vente d’un produit | order_item | Somme des quantité de vente d’un produit |
| avg_cart | Panier moyen | orders | Moyenne montant total par mois |
| new_customers_per_month | Nombre de nouveaux clients par mois | customers | Somme par date d’inscription |
| localisation | Localisation des clients| customers | Pays|

Concept PACE : Planifier, Analyser, Construire, Executer : dans cette séance, on est dans la phase P, Planification du PACE ici

## Séance 2 : Modèles de données et architectures
Création d'un schéma en étoile pour la database ecommerce_dw : fact_sales en table de fait au milieu, reliée par clés aux tables de dimensions orders, customers, et product. Noter les cardinalités 0,1 to many et 1 to many.

Dans cette séance, on est dans la phase A, Analyse du PACE ici : on a modélisé le début de notre planification.

## Séance 3
Exploration de la notion de scalabilité. Création de la database correspondant au schéma à la séance 2 : phase C de Construction du PACE ici

## Séance 4 : analyse et conception
Faire attention aux valeurs aberrantes, null values, doublons, formats, encodages

## Séance 5 Intégration et transformation I
Notions de datalakes, ETL/ELT (passage sur pgadmin/postgresql pour dbt puisque pas de connecteur sur dbt-cloud : database exportée depuis pgadmin, voir fichier )

## Séance 6
Utilisation de dbt-core pour lier la base de données ecommerce depuis postgresql. Staging et tests

## Séance 7: exploitation et gestion 1
Repris la table de la séance 1 pour calculer les KPIs dans pgadmin
| Nom | Table reliée | Comment calculer |
| --- | --- | --- |
| chiffre_affaire_par_mois | orders | SELECT EXTRACT(MONTH FROM order_date), SUM(total_amount) FROM orders GROUP BY EXTRACT(MONTH FROM order_date) |
| sales_volume_per_product | order_item | SELECT SUM(quantity) FROM order_items GROUP BY id_product |
| avg_cart_per_month | orders | SELECT EXTRACT(MONTH FROM order_date), AVG(total_amount) FROM orders GROUP BY EXTRACT(MONTH FROM order_date) |
| new_customers_per_month | customers | SELECT EXTRACT(MONTH FROM signup_date), COUNT(id_customer) FROM customers GROUP BY EXTRACT(MONTH FROM signup_date) |
| customer_per_country | customers | SELECT country, COUNT(id_customer) FROM customers GROUP BY country |

## Séance 8 : Exploitation et gestion II (qualité & monitoring)
Nous sommes enfin dans la phase E du PACE : Executif. On présente les résultats via tableau public, présentation des KPIs calculés dans la séance précédente (voir fichier dashboard)

## Séance 9 : sécurité et contrôle
Focus sur la sécurité. Rôles dans la database pour compartimenter et protéger les données. Masquage des données, par exemple les emails
