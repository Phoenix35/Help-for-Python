# Python cheatsheet
**Cette antisèche (cheatsheet en anglais) sert à référencer les outils de Python
pour un accès rapide.**

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Python cheatsheet](#python-cheatsheet)
- [Avant-propos](#avant-propos)
- [Types de variables](#types-de-variables)
	- [Numérique](#numérique)
		- [Modules utiles](#modules-utiles)
		- [Complexes - `complex`](#complexes---complex)
			- [Propriétés](#propriétés)
			- [Opérateurs](#opérateurs)
			- [Modules](#modules)
		- [Flottants - `float`](#flottants---float)
			- [Propriétés](#propriétés-1)
			- [Opérateurs](#opérateurs-1)
			- [Modules](#modules-1)
		- [Entiers - `int`](#entiers---int)
			- [Propriétés](#propriétés-2)
			- [Opérateurs](#opérateurs-2)
	- [Itérateur](#itérateur)
			- [Concepts](#concepts)
			- [Opérations](#opérations)
			- [Modules](#modules-2)
	- [Séquence](#séquence)
			- [Propriétés](#propriétés-3)
			- [Opérateurs](#opérateurs-3)
		- [Immuable - `tuple`](#immuable---tuple)
		- [Muable - `list`](#muable---list)
		- [Générateur immuable - `range`](#générateur-immuable---range)
		- [Chaine de caractères immuable - `str`](#chaine-de-caractères-immuable---str)
			- [Ordre lexicographique](#ordre-lexicographique)
			- [String formatting](#string-formatting)
	- [Collection](#collection)
		- [Données arbitraires - `dict`](#données-arbitraires---dict)
		- [Données uniques muable - `set`](#données-uniques-muable---set)
		- [Données uniques immuable - `frozenset`](#données-uniques-immuable---frozenset)
	- [Autres types natifs](#autres-types-natifs)
		- [Fonctions](#fonctions)
		- [Type](#type)
			- [None](#none)
		- [Booléens - `True` `False`](#booléens---true-false)
- [Opérateurs](#opérateurs-4)
	- [`bool`](#bool)
		- [`not`](#not)
	- [`is`](#is)
- [Comment bien écrire son code - Best practices](#comment-bien-écrire-son-code---best-practices)
	- [Itérer sur les **indices** d'une *séquence*](#itérer-sur-les-indices-dune-séquence)
	- [Itérer sur les **valeurs** d'une *séquence*](#itérer-sur-les-valeurs-dune-séquence)
	- [Itérer sur les **indices et valeurs** d'une *séquence*](#itérer-sur-les-indices-et-valeurs-dune-séquence)
	- [Itérer sur **plusieurs valeurs à la fois** d'une *séquence*](#itérer-sur-plusieurs-valeurs-à-la-fois-dune-séquence)
	- [Itérer sur les **valeurs** d'un *dictionnaire*](#itérer-sur-les-valeurs-dun-dictionnaire)
	- [Itérer sur les **clés et valeurs** d'un *dictionnaire*](#itérer-sur-les-clés-et-valeurs-dun-dictionnaire)
	- [Itérer sur les **valeurs** d'un *set*](#itérer-sur-les-valeurs-dun-set)

<!-- /TOC -->

# Avant-propos

Si une opération ou un opérateur est présente dans plusieurs sous-classes,
et qu'elle a la même fonctionnalité que la classe dont elle hérite,
elle n'est pas répétée.  
Pour faire un test d'appartenance, il est préférable d'utiliser `isinstance`.

# Types de variables
## Numérique
``` python
2.0 + 0j # complex
2.0      # float
2        # int
```
Ces nombres ont la même valeur mais avec des types de plus en restrictifs.  
Chaque type rajoute une couche d'abstraction.  
On pourra appliquer plus de fonctions
sur les entiers
que sur les flottants
que sur les complexes.  
Pour avoir une hiérarchie, il faudra utiliser `numbers`.  
**Attention** : les calculs se font souvent à virgule flottante
et sont donc **imprécis**.  
`==` est une égalité stricte,
pour une égalité approximative
utiliser la formule `abs(a-b) <= max(1e-09 * max(abs(a), abs(b)), 0)`
ou dès Python 3.5 `math.isclose`.

### Modules utiles
`cmath`, `math`, `numbers`, `numpy`, `scipy`

---
### Complexes - `complex`
Les complexes sont écrits sous la forme `a + bj`  
où `a` et `b` sont des réels  
et `j` est le i classique.

#### Propriétés

| Propriétés / Opérations  | Explication                                                                                | Exemple                                    |
| ------------------------ |:------------------------------------------------------------------------------------------:| ------------------------------------------ |
| x`.real`                 | Retourne la partie réelle                                                                  | `(1 -(1/10) * 1j).real == 1`               |
| x`.imag`                 | Retourne la partie imaginaire                                                              | `(1 -(1/10) * 1j).imag == -0.1`            |
| x`.conjugate()`          | Retourne le complexe conjugué                                                              | `(1 -(1/10) * 1j).conjugate() == 1 +0.1j`  |
| `abs(x)`                 | Retourne la magnitude de `x`                                                               | `abs(1 -(1/10) * 1j) == 1.004987562112089` |
| `complex(re[, im])`      | Retourne le complexe de partie réelle `re` et de partie imaginaire `im`. `im`=0 par défaut | `complex(1, -(1/10)) == 1 -0.1j`           |
| `isinstance(x, complex)` | Retourne `True` si `x` est un complexe, `False` sinon                                      | `isinstance(2.0, complex) == False`        |

#### Opérateurs

| Opérateurs            | Explication                                | Exemple             |
| --------------------- |:------------------------------------------:| ------------------- |
| x `+` y               | Retourne l'addition de deux nombres        |                     |
| x `-` y               | Retourne la soustraction de deux nombres   |                     |
| x `*` y               | Retourne la multiplication de deux nombres |                     |
| x `**` y, `pow(x, y)` | Retourne `x` à la puissance `y`            |                     |
| x `/` y               | Retourne la division de deux nombres       |                     |
| x `==` y              | **Compare** l'égalité de deux nombres      |                     |
| x `!=` y              | **Compare** l'inégalité de deux nombres    |                     |

#### Modules

| Fonctions spécifiques de modules | Explication                                                  | Exemple                                                          |
| -------------------------------- |:------------------------------------------------------------:| ---------------------------------------------------------------- |
| `cmath`                          | Similaire au module `math`, mais travaille sur les complexes | `from cmath import sqrt, phase, polar, rect, pi`                 |
| `cmath.sqrt(x)`                  | Retourne la racine carrée de `x`                             | `sqrt(-1) == 1j`                                                 |
| `cmath.phase(x)`                 | Retourne l'argument (aussi nommé phase) de `x`               | `phase(1 -1j) == -pi/4`                                          |
| `cmath.polar(x)`                 | Retourne `x` en coordonnées polaires sous forme de tuple     | `polar(1 -1j) == (abs(1 -1j), phase(1 -1j)) == (sqrt(2), -pi/4)` |
| `cmath.rect(r, phi)`             | Retourne le complexe de coordonnées polaires (`r`, `phi`)    | `rect(abs(1 -1j), phase(1 -1j)) ≈ 1 -1j`                         |

---
### Flottants - `float`
Hérite de `complex`  
Toute valeur numérique **non complexe** a pour **partie imaginaire 0**
et pour **conjugué elle-même**.  
**Attention** : les calculs se font souvent à virgule flottante
et sont donc **imprécis**.  
`==` signifie ici ≈

#### Propriétés

| Propriétés / Opérations    | Explication                                                                 | Exemple                                          |
| -------------------------- |:---------------------------------------------------------------------------:| ------------------------------------------------ |
| x`.as_integer_ratio()`     | Retourne le dénominateur et le numérateur (si possible)                     | `(-2.5).as_integer_ratio() == (-5, 2)`           |
| x`.is_integer()`           | Retourne `True` si le nombre est un entier, `False` sinon                   | `(-2.5).is_integer() == False`                   |
| `abs(x)`                   | Retourne la valeur absolue de `x`                                           | `abs(-2.5) == 2.5`                               |
| `round(x[, n])`            | Retourne `x` arrondi au `n`-ième chiffre après la virgule. `n`=0 par défaut | `round(pi, 4) == 3.1416`                         |
| `divmod(x, y)`             | Retourne le tuple (`x // y`, `x % y`)                                       | `divmod(-3.4, pi) == (-2.0, 2.8831853071795863)` |
| `float(x)`                 | **Coerce** `x` à un nombre à virgule flottante                              | `float("3.4") == 3.4`                            |
| `isinstance(x, float)`     | Retourne `True` si `x` est un flottant, `False` sinon                       | `isinstance(2.0, float) == True`                 |

#### Opérateurs

| Opérateurs  | Explication                                        | Exemple                           |
| ----------- |:--------------------------------------------------:| --------------------------------- |
| x `//` y    | Retourne la division entière de deux nombres       | `-3.4 // pi == -2.0`              |
| x `%` y     | Retourne le modulo de deux nombres                 | `-3.4 % pi == 2.8831853071795863` |
| x `<` y     | **Compare** l'infériorité stricte de deux nombres  |                                   |
| x `<=` y    | **Compare** l'infériorité de deux nombres          |                                   |
| x `>` y     | **Compare** la supériorité stricte de deux nombres |                                   |
| x `>=` y    | **Compare** la supériorité de deux nombres         |                                   |

#### Modules

| Fonctions spécifiques de modules | Explication                                         | Exemple                               |
| -------------------------------- |:---------------------------------------------------:| ------------------------------------  |
| `math`                           | Le module classique pour travailler sur des nombres | `from math import trunc, floor, ceil` |
| `math.trunc(x)`                  | Retourne `x` tronqué en entier                      | `trunc(-1.1) == -1`                   |
| `math.floor(x)`                  | Retourne le plus petit entier <= `x`                | `floor(-1.1) == -2`                   |
| `math.ceil(x)`                   | Retourne le plus petit entier >= `x`                | `ceil(-1.1) == -1`                    |

`floor` et `ceil` sont lents.
Si la rapidité est un problème, utiliser `// 1` et `// 1 + 1` respectivement.

---
### Entiers - `int`
Hérite de `float`  
Les calculs sur entiers sont **exacts**.

#### Propriétés

| Opérations           | Explication                                                              | Exemple                         |
| -------------------- |:------------------------------------------------------------------------:| ------------------------------- |
| `pow(x, y, z)`       | `x` `y` et `z` doivent être entiers et `y > 0`. Retourne `pow(x, y) % z` | `pow(30, 20, 7) == 4`           |
| `int(x [, base])`    | **Coerce** `x` à un entier en base `base`. `base`=10 par défaut          | `int(3.4) == 3`                 |
| `isinstance(x, int)` | Retourne `True` si `x` est un entier, `False` sinon                      | `isinstance(2.0, int) == False` |

`trunc` utilise la fonction interne `__trunc__()`
alors que `int` utilise `__int__()`.  
Si on veut *juste* **transformer un flottant en entier**,
`trunc` est plus rapide.

#### Opérateurs

| Opérateurs bit-à-bit      | Explication                                     | Exemple |
| ------------------------- |:-----------------------------------------------:| ------- |
| x <code>&verbar;</code> y | Retourne le `OR` de deux entiers                |         |
| x `^` y                   | Retourne le `XOR` de deux entiers               |         |
| x `&` y                   | Retourne le `AND` de deux entiers               |         |
| x `<<` n                  | Left-shift avec perte d'un nombre par un autre  |         |
| x `>>` n                  | Right-shift avec perte d'un nombre par un autre |         |
| ~x                        | Inverse les bits d'un nombre                    |         |

---

---

## Itérateur

Un itérateur est un type de données
sur lequel peut être utilisé les concepts d'itérations.  
C'est la base de la boucle `for`.

#### Concepts
Un item est un élément d'un itérateur.  
Les deux termes seront utilisés de manière interchangeable.

| Concepts           | Explication                                                   | Exemple                       |
| ------------------ |:-------------------------------------------------------------:| ----------------------------- |
| `for elm in x`     | Itère sur l'itérateur `x`, chaque item aura pour valeur `elm` | `for elm in x:`               |
| `in`               | Vérifie l'appartenance                                        | `('a' in 'abc') == True`      |
| `not in`           | Contraire de `in`                                             | `('a' not in 'abc') == False` |

#### Opérations

| Opérations                     | Explication                                                                                                                                                            | Exemple                                                                                       |
| ------------------------------ |:----------------------------------------------------------------------------------------------------------------------------------------------------------------------:| --------------------------------------------------------------------------------------------- |
| `all(it)`                      | Retourne `True` si tous les éléments de `it` sont vrai, `False` sinon                                                                                                  | `all([not False, not 0, not '']) == True`                                  |
| `any(it)`                      | Retourne `True` si au moins un élément de `it` est vrai, `False` sinon                                                                                                 | `any([False, 0, '']) == False`                                             |
| `next(it[, default])`          | Retourne le prochain item de `it`, ou `défault` à défaut                                                                                                               | `next(x**2 for x in range(5, 10) if not x % 2) == 36`                      |
| `enumerate(it[, start])`       | Retourne un itérateur de tuples (indice + `start`, valeur). `start`=0 par défaut                                                                                       | `a = enumerate([5, 4]); next(a) == (0, 5)`                                 |
| `filter(function, it)`         | Construit un itérateur à partir des éléments de `it` qui vérifient `function`. Si function a la valeur particulière `None`, équivaut à `(item for item in it if item)` | `filter(function, it) == (item for item in it if function(item))`          |
| `map(function, it, ...)`       | Retourne un itérateur qui applique `function` aux arguments données                                                                                                    | `a = map(lambda x, y: x*y, (1, 2, 3), (4, 5, 6)); tuple(a) == (4, 10, 18)` |
| `min(it[, key])`               | Retourne le plus petit item de `it` trié selon `key`. `key`=ordre lexicographique par défaut                                                                           | `min([1, 2, 3]) == 1`                                                      |
| `max(it[, key])`               | Retourne le plus grand item de `it` trié selon `key`. `key`=ordre lexicographique par défaut                                                                           | `max([1, 2, 3]) == 3`                                                      |
| `sorted(it[, key][, reverse])` | Retourne une **liste** d'items de `it` trié selon `key`. `key`=ordre lexicographique par défaut                                                                        | `sorted(range(2)) == [0, 1]`                                               |
| `zip(*it, ...)` | Retourne un itérateur de tuples agrégeant chaque itérable                                                                        																											| `a = zip((1, 2), (3, 4)); next(a) == (1, 3); next(a) == (2, 4)`            |
| `iter(object[, sentinel])`     | Transforme un objet en itérateur jusqu'à ce qu'un élément vaille sentinel                                                                                              | Voir [la méthode iter][itermethod]                                         |

Note : un générateur a la même syntaxe qu'une compréhension de liste
(voir l'exemple de `next`).

[itermethod]: <https://docs.python.org/3.4/library/functions.html#iter>

#### Modules
`itertools`

---

---
## Séquence
Une séquence est un itérateur **ordonnée** :
les items peuvent être retrouvés à l'aide d'entiers appelés **indices**.

#### Propriétés

| Propriétés / Opérations    | Explication                                                                                                                                                                    | Exemple                         |
| -------------------------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:| ------------------------------- |
| seq`[i]`                   | Retourne le `i`-ème élément de la séquence                                                                                                                                     | `[1, 2, 3] [1] == 2`            |
| seq`[ [i [: j [:k]]] ]`    | Retourne la séquence coupé (*slice*) de `i` **inclus** à `j` **exclu** de pas `k`. `i`=*départ*, `j`=*arrivée*, `k`=1 par défaut. Si k est > 0, *départ*=0 et *arrivée*=len(s) | `[1, 2, 3] [1:] == [2, 3]`      |
| `len(seq)`                 | Retourne la taille (longueur) de la séquence `s`                                                                                                                               | `len( [1, 2, 3] ) == 3`         |
| `reversed(seq)`            | Retourne `seq` inversée                                                                                                                                                        | `next(reversed(range(2))) == 1` |
| seq.`index(x [, i [, j]])` | Retourne l'indice de la première occurence de `x` à partir de l'indice `i` et avant `j`. `ValueError` si l'élément n'est pas trouvé. `i`=0, `j`=len(s) par défaut              | `[1, 2, 3].index(2) == 1`       |
| seq.`count(x)`             | Retourne le nombre d'occurences de `x`                                                                                                                                         | `[1, 2, 3].count(15) == 0`      |

#### Opérateurs

| Opérateurs            | Explication                                                                                                                                     | Exemple                  |
| --------------------- |:-----------------------------------------------------------------------------------------------------------------------------------------------:| ------------------------ |
| s `==` t              | **Compare** l'égalité de type, puis de taille, puis de valeurs de deux séquences                                                                | `((1,) == [1]) == False` |
| s `!=` t              | **Compare** l'inégalité de type, puis de taille, puis de valeurs de deux séquences                                                              | `((1,) != [1]) == True`  |
| s `+` t               | Retourne la concaténation de deux séquences **de même type**. Ne marche pas pour `range`. **Il ne faut pas concaténer des séquences immuables** | `[1] + [3] == [1, 3]`    |
| s `* n`               | Retourne `n` références d'une séquence. `n` est un entier. S'il est négatif, il est traité comme 0. Ne marche pas pour `range`                  | `(1,) * 3 == (1, 1, 1)`  |

Les opérateurs de comparaison `<`, `<=`, `>`, `>=`
ne s'appliquent que sur les séquences **de même type**
et utilisent l'[**ordre lexicographique**](#ordre-lexicographique)

### Immuable - `tuple`
La séquence immuable (*immutable* en anglais) la plus simple est un `tuple`.  
Les séquences immuables ne peuvent pas être modifiées.  
Elles supportent le hash, et peuvent donc être utilisées pour
des clés de dictionnaires
et dans des sets.
**Concaténation** : utiliser la propriété `extend` d'une liste.


### Muable - `list`
TODO

### Générateur immuable - `range`
TODO


### Chaine de caractères immuable - `str`
TODO

#### Ordre lexicographique
- le même ordre que le premier élément inégal :
`[1, 5] > [1, 2, 8]` car `5 != 2`, donc on utilise l'ordre `5 > 2`
- si l'élément n'existe pas, la séquence la plus courte est ordonnée avant
`[1, 2] < [1, 2, 3]`
- `'0' < '9' < 'A' < 'Z' < 'a' < 'z' < 'À' < 'Ý' < 'à' < 'ÿ'`

#### String formatting
TODO

## Collection
### Données arbitraires - `dict`
TODO

### Données uniques muable - `set`
TODO

### Données uniques immuable - `frozenset`
TODO

## Autres types natifs
### Fonctions
TODO

### Type
TODO

#### None
TODO

### Booléens - `True` `False`
TODO

# Opérateurs

## `bool`
TODO

### `not`
TODO

## `is`
TODO

# Comment bien écrire son code - Best practices

## Itérer sur les **indices** d'une *séquence*
On a **très rarement** besoin de faire ça, en général on veut les valeurs.
``` python
for i in range(len(seq)):
		# i est l'indice
```

## Itérer sur les **valeurs** d'une *séquence*
``` python
for v in seq:
		# v est l'élément
```

## Itérer sur les **indices et valeurs** d'une *séquence*
``` python
for i, v in enumerate(seq):
		# i est l'indice
		# v est l'élément
```

## Itérer sur **plusieurs valeurs à la fois** d'une *séquence*
``` python
# On slice la séquence
# tous les n
for liste_v in (seq[i : i + n] for i in range(0, len(seq), n)):
		# liste_v est une liste qui contient n éléments
```

## Itérer sur les **clés** d'un *dictionnaire*
``` python
# NOTE : sur une séquence ou un set, k contiendrait la valeur
for k in dico:
		# k est la clé ("l'indice")
```

## Itérer sur les **valeurs** d'un *dictionnaire*
``` python
for v in dico.values():
		# v est la valeur
```

## Itérer sur les **clés et valeurs** d'un *dictionnaire*
``` python
for k, v in dico.items():
		# k est la clé
		# v est la valeur
```

## Itérer sur les **valeurs** d'un *set*
``` python
for v in s:
		# v est la valeur
```
