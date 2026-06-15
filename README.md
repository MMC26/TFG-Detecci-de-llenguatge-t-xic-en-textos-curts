# Detecció de llenguatge tòxic en textos curts

Aquest repositori conté el codi desenvolupat per al Treball de Fi de Grau **Detecció de llenguatge tòxic en textos curts**, realitzat en el Grau en Matemàtica Computacional i Analítica de Dades de la Universitat Autònoma de Barcelona.

L’objectiu del projecte és desenvolupar i analitzar un sistema de classificació binària capaç de distingir entre textos tòxics i no tòxics mitjançant models clàssics de machine learning basats en representacions textuals interpretables.

## Descripció del projecte

El treball compara diferents models de classificació:

* Logistic Regression
* Linear SVM
* Multinomial Naive Bayes
* Complement Naive Bayes
* Bernoulli Naive Bayes

Els textos es representen mitjançant:

* Bag-of-Words
* TF-IDF
* N-grams de paraula
* N-grams de caràcter

El projecte també estudia:

* La cerca d’hiperparàmetres mitjançant validació creuada.
* L’ajust del llindar de decisió.
* L’impacte de l’eliminació de stopwords.
* La generalització entre datasets i el domain shift.
* L’adaptació de domini amb una fracció de dades de Jigsaw.
* La interpretabilitat del model mitjançant els coeficients dels n-grams.
* L’anàlisi qualitativa de falsos positius i falsos negatius.
* El comportament del model davant del sarcasme i el llenguatge no literal.

## Model final

El model final seleccionat és un **Linear SVM** que combina:

* N-grams de paraula d’ordre 1 i 2.
* N-grams de caràcter de longitud entre 3 i 5.
* Ajust del llindar de decisió mitjançant validació creuada.

La selecció es basa en un compromís entre el rendiment en el domini original i la capacitat de generalització a un domini diferent.

## Resultats principals

| Conjunt de dades                                  | F1-macro |
| ------------------------------------------------- | -------: |
| Dataset principal                                 |    0.922 |
| Jigsaw                                            |    0.691 |

Els resultats mostren un rendiment elevat en l’avaluació in-domain, però una disminució quan el model s’aplica als comentaris de Jigsaw. Aquesta diferència està relacionada amb el canvi de domini, la distribució de les classes i les diferències en els criteris d’etiquetatge.

## Datasets

Els datasets no s’inclouen directament en aquest repositori. S’han de descarregar des de les fonts originals.

### Dataset principal

**Hate Speech and Offensive Language Dataset**

https://www.kaggle.com/datasets/mrmorj/hate-speech-and-offensive-language-dataset

Fitxer utilitzat:

```text
labeled_data.csv
```

Les etiquetes originals s’han agrupat de la manera següent:

* `hate speech` i `offensive language` → tòxic (`1`)
* `neither` → no tòxic (`0`)

### Jigsaw Toxic Comment Classification Challenge

https://www.kaggle.com/datasets/julian3833/jigsaw-toxic-comment-classification-challenge

Fitxer utilitzat:

```text
train.csv
```
En la configuració principal, un comentari es considera tòxic quan presenta l’etiqueta `toxic` o `severe_toxic`.

### Balanced Sarcasm Dataset

https://www.kaggle.com/datasets/danofer/sarcasm

Fitxer utilitzat:

```text
train-balanced-sarcasm.csv
```

Aquest dataset s’utilitza únicament com a conjunt de prova d’estrès per comparar la taxa de prediccions tòxiques entre textos sarcàstics i no sarcàstics.

### The Best Sarcasm Annotated Dataset in Spanish

https://www.kaggle.com/datasets/mikahama/the-best-sarcasm-annotated-dataset-in-spanish

Fitxer utilitzat:

```text
sarcasmo.tsv
```

Aquest dataset s’utilitza com a prova addicional per estudiar el comportament del model davant del sarcasme en castellà.


## Requisits

El projecte utilitza Python 3 i les llibreries següents:

```text
pandas
numpy
scikit-learn
matplotlib
scipy
wordcloud
```

Les dependències es poden instal·lar executant:

```bash
pip install -r requirements.txt
```

També es poden instal·lar directament:

```bash
pip install pandas numpy scikit-learn matplotlib scipy wordcloud
```

## Execució

El codi està preparat principalment per executar-se a Google Colab.

1. Descarregar els quatre datasets.
2. Guardar-los a Google Drive.
3. Obrir el notebook:

```text
deteccio_llenguatge_toxic.ipynb
```

4. Modificar les rutes dels datasets si és necessari.
5. Executar les cel·les en ordre.

Les rutes originals del notebook tenen el format següent:

```python
"/content/drive/MyDrive/TFG/..."
```
En cas d’executar el codi a Google Colab, normalment no és necessari instal·lar manualment les llibreries, ja que la majoria ja estan disponibles a l’entorn. En canvi, si s’executa en local, cal instal·lar les dependències indicades al fitxer requirements.txt i adaptar tant la forma d’accés als datasets com les rutes utilitzades al notebook.

## Contingut del notebook

El notebook segueix les fases següents:

1. Càrrega i unificació de les etiquetes.
2. Anàlisi exploratòria de les dades.
3. Neteja i preprocessament dels textos.
4. Construcció de representacions Bag-of-Words i TF-IDF.
5. Entrenament dels models baseline.
6. Cerca d’hiperparàmetres amb validació creuada.
7. Avaluació en el dataset principal.
8. Avaluació out-of-domain en Jigsaw.
9. Experiments amb el llindar de decisió i n-grams de caràcter.
10. Experiment d’eliminació de stopwords.
11. Adaptació de domini amb dades de Jigsaw.
12. Interpretació dels coeficients del model.
13. Anàlisi de falsos positius i falsos negatius.
14. Proves d’estrès amb sarcasme en anglès i castellà.

## Consideracions

Els datasets de sarcasme no contenen etiquetes de toxicitat. Per aquest motiu, les prediccions del model no s’interpreten directament com a falsos positius o falsos negatius. En aquests experiments s’analitza la taxa de textos classificats com a tòxics i es realitza una interpretació qualitativa dels exemples.

## Autoria

**Maria Muñoz Cabestany**

Treball de Fi de Grau
Grau en Matemàtica Computacional i Analítica de Dades
Universitat Autònoma de Barcelona
Curs 2025–2026

## Finalitat

Aquest repositori s’ha desenvolupat amb finalitats acadèmiques.
