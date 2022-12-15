
# Nombre de fiches d'observations : 

Pour ouvrir le fichier selection.json, le language python a été utilisé. Le code ci-dessous a permis d'importer les données de ce fichier dans l'objet *data*, la fonction read.json permet d'importer le fichier *selection.json* en panda dans python. Ceci facilitera la manipulation des données par la suite : 

```
import json
data = pd.read_json("C:/Users/Marjo/Desktop/tests/selection.json")

data

```

Ce fichier est composé de 9 609 vidéos, informations qui est indiqué à côté de *fileType: MP4*. Dans ces vidéos, il y a 6 026 renards, 1098 loups, 975 bouquetins, 836 blaireaux,  577 fouines et 97 marmottes. 

```
data 

len(data)

```

Pour observer les sites les plus riches en faune sauvage, j'ai filtré les données à partir de la colonne *multispecies* de ma tabla *data*. Il y a 67 vidéos où l'on observe plusieurs espèces. Pour plus facilement observer les caractéristiques de ces données j'ai créé un filtre pour extraire seulement les lignes où plusieurs espèces étaient présentes. Une fois ces 67 observations extraites, avec la colonne *comments*, selon la colonne *path*, la maille 7 a la plus grande richesse spécifique en comptant 3 espèces différentes : 4 bouquetins, 1 chamois et 1 marmotte. A noter, qu'il y a des vidéos avec des oiseaux et que l'espèce n'est pas spécifiée. Pour obtenir cette information le code suivant a été utilisé : 


```

data["multispecies"].value_counts()
data_mask = data["multispecies"]==1
filter_data = data[data_mask]

```

Pour connaitre les vidéos où l'on compte le plus grand nombre d'indidivus de l'espèce identifiée d'après la colonne *species*, nous pouvons compter les valeurs de la colonne *populations* cette colonne. La maille 7 identifie le plus grand nombre avec 19 bouquetins observés (vidéos 122 et 134). Ensuite, la maille 38 (vidéos 1257 et 1258) comptent chacune 17 bouquetins. La maille 9 (vidéos 129 à 132 et 1273 à 1276) comptent 9 bouquetins. Ensuite, il y a la maille 6, 51, 66, 21, 39 qui des observations de 5 individus puis la maille 55 qui comptent des observations de 4 individus. D'autres mailles relèvent ce même nombre d'individus.

ce sont les 12 vidéos qui sont les plus riches en faune. Le code suivant a permis d'obtenir ces informations : 

```
data["population"].value_counts(ascending=True)
values = [11,19,17,9,8,7,6,5,4]
faune = data[data.population.isin(values)]
faune

```

La plus grande meute de loups observée est de 7, elles se trouvent dans les mailles 6 et 21 (vidéos 41,42,482,483). La maille 66 (vidéo 4 855) compte 6 loups. Il y a, entre autres, les mailles 7,39,55,70,72,86,87 qui comptent 5 loups. Ceci permet d'obtenir ces 10 sites où ces observations ont été faites : 

```

data_loup = data["species"]=="loup"
filter_data = data[data_loup]
filter_data["population"].value_counts()
values_loup=[6,7,5]
loup = filter_data[filter_data.population.isin(values_loup)]
loup

```
Ci-dessous l'historgamme de la fréquence de passage des loups en fonction des heures et du mois de l'année. Les loups seraient principalement passés entre 1 heure et 3 heure du matin, le nombre de passage diminue ensuite. D'autres passages ont aussi été observés entre 22h et 23h. Les passages ont été observés au mois d'octobre, novembre, décembre, janvier et février. 

(C:/Users/Marjo/Desktop/tests/histogramme.png)

Le code pour trier et représenter les heures et mois de passages sous forme d'un histogramme : 

```

data_loup = data["species"]=="loup"
filter_data = data[data_loup]
filter_data["population"].value_counts()
values_loup=[6,7,5]
loup = filter_data[filter_data.population.isin(values_loup)]
loup['Datetime'] = pd.to_datetime(loup['startTime'])

loup["Datetime"].groupby([loup["Datetime"].dt.hour.rename("(Heure"), loup["Datetime"].dt.month.rename("Mois)")]).count().plot(kind="bar")

```

Pour le site le plus fréquenté, avec 7 loups filmés, leur passage a été filmé à 2h du matin pour la maille 21 et 8h du matin pour la maille 6. Toutes ces observations ont été relevés au mois de novembre 

(C:/Users/Marjo/Desktop/tests/histogramme_site_max.png)

Le code pour trier et représenter les heures et mois de passages sous forme d'un histogramme : 

```
site_loup=[7]
loup_max = filter_data[filter_data.population.isin(site_loup)]
loup_max['Datetime'] = pd.to_datetime(loup_max['startTime'])

loup_max["Datetime"].groupby([loup["Datetime"].dt.hour.rename("(Heure"), loup["Datetime"].dt.month.rename("Mois)")]).count().plot(kind="bar")

```

1.c) Pour observer la période à laquelle le site est filmé, il serait possible de trier les sites par mois pour relevés l'espèce et son nombre relevé par les vidéos


- [titre 1](#titre-1)
  - [titre 2](#titre-2)
    - [titre 3](#titre-3)


# titre 1
## titre 2
### titre 3

* un item de liste
    * un sous item de liste 
        * etc

*italique*

**gras**

***gras italique***

[un lien html](https://innersource.soprasteria.com/acoss/sdit/repo_documentaire_nga)

> citation 

    Note

```code```

```
code
code

```

* [ ] une checkbox vide
* [x] une chec