
# 🩺 Dr Death – Analyse avec Power BI

## 🎯 Objectif

Ce projet vise à répondre à la question suivante :

**Quels types de personnes Harold Shipman a-t-il assassinées, et quand sont-elles mortes ?**

Nous analysons les données liées aux décès pour détecter des schémas suspects et les comparer à ceux d'autres médecins généralistes.

---

## 🔎 Contexte

Harold Shipman, médecin britannique respecté en apparence, a assassiné plus de 215 patients entre 1975 et 1998 en leur administrant une surdose d’opiacés. L’analyse de son comportement peut nous aider à comprendre comment les données auraient pu alerter les autorités plus tôt.

---

## 📁 Données utilisées

- `shipman-confirmed-victims.csv` : liste des victimes confirmées, avec leur date de décès, âge, etc.
- `shipman-times-comparison.csv` : comparaison des heures de décès entre Shipman et d'autres médecins.

---

## 🛠 Outils et méthode

### 🧠 Power BI
Power BI est un outil de visualisation de données développé par Microsoft :
- Visualisations dynamiques et interactives
- Connexion à plusieurs types de sources
- Utilisation de Power Query pour le nettoyage
- DAX pour les mesures personnalisées

### 📊 Analyses menées
À partir des données et de l'analyse Python, nous avons visualisé dans Power BI :

1. **Répartition des victimes par âge et sexe**
2. **Décès par année, mois et jour de la semaine**
3. **Heure des décès comparée aux autres médecins**
4. **Filtrage par tranche d’âge, année, sexe**

---

## 🧪 Résultats clés issus de Jupyter

# Dr Death – Analyse Statistique avec Jupyter (VS Code)

Ce notebook analyse deux jeux de données liés aux victimes du Dr Harold Shipman, considéré comme le tueur en série le plus prolifique du Royaume-Uni.

### Objectif
Répondre à la question : **Quels types de personnes Harold Shipman a-t-il assassinées, et quand sont-elles mortes ?**

---

## 📌 Conclusion

- La majorité des victimes sont des femmes âgées.
- Les décès sont particulièrement nombreux entre 1993 et 1998.
- Les décès se produisent souvent en semaine, pendant les heures de travail.
- Les horaires de décès sous Shipman présentent un schéma distinct de celui des autres médecins.

Ces éléments renforcent l'hypothèse d'un comportement prémédité et organisé.

---

---

## 🔍 Exemple de code Python utilisé

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

sns.set(style="whitegrid")
plt.rcParams['figure.figsize'] = (10, 6)

```

```python
# Définir les chemins
victims_path = r"C:\Users\microstar\Desktop\Git Hub\Dr Death\shipman-confirmed-victims.csv"
times_path = r"C:\Users\microstar\Desktop\Git Hub\Dr Death\shipman-times-comparison.csv"

# Chargement
df_victims = pd.read_csv(victims_path)
df_times = pd.read_csv(times_path)

df_victims.columns = df_victims.columns.str.strip()
df_victims['DateofDeath'] = pd.to_datetime(df_victims['DateofDeath'], errors='coerce')
df_victims['Year'] = df_victims['DateofDeath'].dt.year
df_victims['Month'] = df_victims['DateofDeath'].dt.month
df_victims['Weekday'] = df_victims['DateofDeath'].dt.day_name()

df_victims.head()
```

```python
df_victims.describe()
```

```python
sns.histplot(df_victims['Age'], bins=20, kde=True)
plt.title("Distribution des âges des victimes")
plt.xlabel("Âge")
plt.ylabel("Nombre")
plt.show()
```

```python
df_victims['Year'].value_counts().sort_index().plot(kind='bar')
plt.title("Nombre de décès par année")
plt.xlabel("Année")
plt.ylabel("Nombre de victimes")
plt.show()
```

```python
sns.countplot(x='gender', data=df_victims)
plt.title("Répartition des victimes par genre")
plt.show()
```

```python
order = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
sns.countplot(data=df_victims, x='Weekday', order=order)
plt.title("Décès par jour de la semaine")
plt.xticks(rotation=45)
plt.show()
```

```python
df_times.columns = df_times.columns.str.strip()
df_times['Doctor'].value_counts()
```

```python
sns.histplot(data=df_times, x='Time of death', hue='Doctor', multiple='stack')
plt.title("Comparaison des horaires de décès (Shipman vs autres)")
plt.xticks(rotation=45)
plt.show()
```

---

## 🖼 Captures d’écran (à insérer)

- Histogramme des âges
- Courbe des décès par an
- Camembert de la répartition hommes/femmes
- Graphique des décès par heure (comparatif)
- Carte de chaleur des jours de décès

---

## 📌 Conclusion

- Les victimes sont majoritairement des femmes âgées.
- Shipman agissait principalement entre 1993 et 1998.
- Les décès surviennent surtout les jours ouvrés, souvent l'après-midi.
- Les schémas temporels se distinguent nettement de ceux des autres médecins.

---

## 📚 Ressources complémentaires

- [Documentation Microsoft Power BI](https://learn.microsoft.com/fr-fr/power-bi/)
- [NewScientist – Statistics could have spotted mass murderer](https://www.newscientist.com/article/dn7958-statistics-could-have-spotted-mass-murderer/)
- [Tutoriel YouTube Power BI (FR)](https://www.youtube.com/watch?v=TmhQCQr_DCA)

