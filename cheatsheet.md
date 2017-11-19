<!--
  Replace
  &verbar;
  |
  -->
<!--
  Replace
  <td><code> </code></td>
  <td></td>
  -->

# Python cheatsheet
**Cette antisèche (cheatsheet en anglais) sert à référencer les outils de Python
pour un accès rapide.**

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Python cheatsheet](#python-cheatsheet)
	- [Avant-propos](#avant-propos)
	- [Types de variables](#types-de-variables)
		- [Numérique](#numrique)
			- [Modules utiles](#modules-utiles)
			- [Complexes - `complex`](#complexes-complex)
				- [Propriétés](#proprits)
				- [Opérateurs](#oprateurs)
				- [Modules](#modules)
			- [Flottants - `float`](#flottants-float)
				- [Propriétés](#proprits)
				- [Opérateurs](#oprateurs)
				- [Modules](#modules)
			- [Entiers - `int`](#entiers-int)
				- [Propriétés](#proprits)
				- [Opérateurs](#oprateurs)
		- [Itérateur](#itrateur)
				- [Concepts](#concepts)
		- [Séquence](#squence)
				- [Propriétés](#proprits)
				- [Opérateurs](#oprateurs)
			- [Muable - `list`](#muable-list)
			- [Immuable - `tuple`](#immuable-tuple)
			- [Suite de nombres immuable - `range`](#suite-de-nombres-immuable-range)
			- [Chaine de caractères immuable - `str`](#chaine-de-caractres-immuable-str)
				- [Ordre lexicographique](#ordre-lexicographique)
				- [String formatting](#string-formatting)
		- [Collection](#collection)
			- [Données arbitraires - `dict`](#donnes-arbitraires-dict)
			- [Données uniques muable - `set`](#donnes-uniques-muable-set)
			- [Données uniques immuable - `frozenset`](#donnes-uniques-immuable-frozenset)
		- [Autres types natifs](#autres-types-natifs)
			- [Fonctions](#fonctions)
			- [Type](#type)
				- [None](#none)
			- [Booléens - `True` `False`](#boolens-true-false)
	- [Opérateurs](#oprateurs)
		- [`bool`](#bool)
			- [`not`](#not)
		- [`is`](#is)
	- [Fonctions natives](#fonctions-natives)
		- [`all`](#all)
		- [`any`](#any)
		- [`bool`](#bool)

<!-- /TOC -->

---

---

---
## Avant-propos

Si une opération ou un opérateur est présente dans plusieurs sous-classes,
et qu'elle a la même fonctionnalité que la classe dont elle hérite,
elle n'est pas répétée.  
Pour faire un test d'appartenance, il est préférable d'utiliser `isinstance`.

---

---

---
## Types de variables
### Numérique
``` python
2.0 + 0j # complex
2.0      # float
2        # int
```
Ces nombres ont la même valeur mais avec des types de plus en restrictifs.  
Chaque type rajoute une couche d'abstraction.  
On pourra appliquer plus de fonctions sur les entiers que sur les flottants que sur les complexes.  
Pour avoir une hiérarchie, il faudra utiliser `numbers`.  
**Attention** : les calculs se font souvent à virgule flottante
et sont donc **imprécis**.  
`==` est une égalité stricte,
pour une égalité approximative
utiliser la formule `abs(a-b) <= max(1e-09 * max(abs(a), abs(b)), 0)`
ou dès Python 3.5 `math.isclose`.

#### Modules utiles
`cmath`, `math`, `numbers`, `numpy`, `scipy`

---
#### Complexes - `complex`
Les complexes sont écrits sous la forme `a + bj`  
où `a` et `b` sont des réels  
et `j` est le i classique.

##### Propriétés

| Propriétés / Opérations  | Explication                                                                                | Exemple                                    |
| ------------------------ |:------------------------------------------------------------------------------------------:| ------------------------------------------ |
| `x.real`                 | Retourne la partie réelle                                                                  | `(1 -(1/10) * 1j).real == 1`               |
| `x.imag`                 | Retourne la partie imaginaire                                                              | `(1 -(1/10) * 1j).imag == -0.1`            |
| `x.conjugate()`          | Retourne le complexe conjugué                                                              | `(1 -(1/10) * 1j).conjugate() == 1 +0.1j`  |
| `abs(x)`                 | Retourne la magnitude de `x`                                                               | `abs(1 -(1/10) * 1j) == 1.004987562112089` |
| `complex(re[, im])`      | Retourne le complexe de partie réelle `re` et de partie imaginaire `im`. `im`=0 par défaut | `complex(1, -(1/10)) == 1 -0.1j`           |
| `isinstance(x, complex)` | Retourne `True` si `x` est un complexe, `False` sinon                                      | `isinstance(2.0, complex) == False`        |

##### Opérateurs

| Opérateurs            | Explication                                | Exemple             |
| --------------------- |:------------------------------------------:| ------------------- |
| x `+` y               | Retourne l'addition de deux nombres        |                     |
| x `-` y               | Retourne la soustraction de deux nombres   |                     |
| x `*` y               | Retourne la multiplication de deux nombres |                     |
| x `**` y, `pow(x, y)` | Retourne `x` à la puissance `y`            |                     |
| x `/` y               | Retourne la division de deux nombres       |                     |
| x `==` y              | **Compare** l'égalité de deux nombres      |                     |
| x `!=` y              | **Compare** l'inégalité de deux nombres    | ` `                 |

##### Modules

| Fonctions spécifiques de modules | Explication                                                  | Exemple                                                          |
| -------------------------------- |:------------------------------------------------------------:| ---------------------------------------------------------------- |
| `cmath`                          | Similaire au module `math`, mais travaille sur les complexes | `from cmath import sqrt, phase, polar, rect, pi`                 |
| `cmath.sqrt(x)`                  | Retourne la racine carrée de `x`                             | `sqrt(-1) == 1j`                                                 |
| `cmath.phase(x)`                 | Retourne l'argument (aussi nommé phase) de `x`               | `phase(1 -1j) == -pi/4`                                          |
| `cmath.polar(x)`                 | Retourne `x` en coordonnées polaires sous forme de tuple     | `polar(1 -1j) == (abs(1 -1j), phase(1 -1j)) == (sqrt(2), -pi/4)` |
| `cmath.rect(r, phi)`             | Retourne le complexe de coordonnées polaires (`r`, `phi`)    | `rect(abs(1 -1j), phase(1 -1j)) ≈ 1 -1j`                         |

---
#### Flottants - `float`
Hérite de `complex`  
Toute valeur numérique **non complexe** a pour **partie imaginaire 0**
et pour **conjugué elle-même**.  
**Attention** : les calculs se font souvent à virgule flottante
et sont donc **imprécis**.  
`==` signifie ici ≈

##### Propriétés

| Propriétés / Opérations    | Explication                                                                 | Exemple                                          |
| -------------------------- |:---------------------------------------------------------------------------:| ------------------------------------------------ |
| `x.as_integer_ratio()`     | Retourne le dénominateur et le numérateur (si possible)                     | `(-2.5).as_integer_ratio() == (-5, 2)`           |
| `x.is_integer()`           | Retourne `True` si le nombre est un entier, `False` sinon                   | `(-2.5).is_integer() == False`                   |
| `abs(x)`                   | Retourne la valeur absolue de `x`                                           | `abs(-2.5) == 2.5`                               |
| `round(x[, n])`            | Retourne `x` arrondi au `n`-ième chiffre après la virgule. `n`=0 par défaut | `round(pi, 4) == 3.1416`                         |
| `divmod(x, y)`             | Retourne le tuple (`x // y`, `x % y`)                                       | `divmod(-3.4, pi) == (-2.0, 2.8831853071795863)` |
| `float(x)`                 | **Coerce** `x` à un nombre à virgule flottante                              | `float("3.4") == 3.4`                            |
| `isinstance(x, float)`     | Retourne `True` si `x` est un flottant, `False` sinon                       | `isinstance(2.0, float) == True`                 |

##### Opérateurs

| Opérateurs  | Explication                                        | Exemple                           |
| ----------- |:--------------------------------------------------:| --------------------------------- |
| x `//` y    | Retourne la division entière de deux nombres       | `-3.4 // pi == -2.0`              |
| x `%` y     | Retourne le modulo de deux nombres                 | `-3.4 % pi == 2.8831853071795863` |
| x `<` y     | **Compare** l'infériorité stricte de deux nombres  |                                   |
| x `<=` y    | **Compare** l'infériorité de deux nombres          |                                   |
| x `>` y     | **Compare** la supériorité stricte de deux nombres |                                   |
| x `>=` y    | **Compare** la supériorité de deux nombres         | ` `                               |

##### Modules

| Fonctions spécifiques de modules | Explication                                         | Exemple                               |
| -------------------------------- |:---------------------------------------------------:| ------------------------------------  |
| `math`                           | Le module classique pour travailler sur des nombres | `from math import trunc, floor, ceil` |
| `math.trunc(x)`                  | Retourne `x` tronqué en entier                      | `trunc(-1.1) == -1`                   |
| `math.floor(x)`                  | Retourne le plus petit entier <= `x`                | `floor(-1.1) == -2`                   |
| `math.ceil(x)`                   | Retourne le plus petit entier >= `x`                | `ceil(-1.1) == -1`                    |
`floor` et `ceil` sont lents.
Si la rapidité est un problème, utiliser `// 1` et `// 1 + 1` respectivement.

---

#### Entiers - `int`
Hérite de `float`  
Les calculs sur entiers sont **exacts**.

##### Propriétés

| Opérations           | Explication                                                              | Exemple                         |
| -------------------- |:------------------------------------------------------------------------:| ------------------------------- |
| `pow(x, y, z)`       | `x` `y` et `z` doivent être entiers et `y > 0`. Retourne `pow(x, y) % z` | `pow(30, 20, 7) == 4`           |
| `int(x [, base])`    | **Coerce** `x` à un entier en base `base`. `base`=10 par défaut          | `int(3.4) == 3`                 |
| `isinstance(x, int)` | Retourne `True` si `x` est un entier, `False` sinon                      | `isinstance(2.0, int) == False` |
`trunc` utilise la fonction interne `__trunc__()`
alors que `int` utilise `__int__()`.  
Si on veut *juste* **transformer un flottant en entier**,
`trunc` est plus rapide.

##### Opérateurs

| Opérateurs bit-à-bit  | Explication                                     | Exemple |
| --------------------- |:-----------------------------------------------:| ------- |
| x `&verbar;` y        | Retourne le `OR` de deux entiers                |         |
| x `^` y               | Retourne le `XOR` de deux entiers               |         |
| x `&` y               | Retourne le `AND` de deux entiers               |         |
| x `<<` n              | Left-shift avec perte d'un nombre par un autre  |         |
| x `>>` n              | Right-shift avec perte d'un nombre par un autre |         |
| ~x                    | Inverse les bits d'un nombre                    | ` `     |

---

---

### Itérateur
Un itérateur est un type de données
sur lequel peut être utilisé les concepts d'itérations.  
C'est la base de la boucle `for`.

##### Concepts
Un item est un élément d'un itérateur.  
Les deux termes seront utilisés de manière interchangeable.

| Concepts           | Explication                                                   | Exemple                       |
| ------------------ |:-------------------------------------------------------------:| ----------------------------- |
| `for`              | Itère sur l'itérateur `x`, chaque item aura pour valeur `elm` | `for elm in x:`               |
| `in`               | Vérifie l'appartenance                                        | `('a' in 'abc') == True`      |
| `not in`           | Contraire de `in`                                             | `('a' not in 'abc') == False` |

---

---
### Séquence
Une séquence est un itérateur **ordonnée** :
les items peuvent être retrouvés à l'aide d'entiers appelés **indices**.

##### Propriétés

| Propriétés / Opérations  | Explication                                                                                                                                                                    | Exemple                    |
| ----------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:| --------------------------------- |
| s`[i]`                   | Retourne le `i`-ème élément de la séquence                                                                                                                                     | `[1, 2, 3] [1] == 2`       |
| s`[ [i [: j [:k]]] ]`    | Retourne la séquence coupé (*slice*) de `i` **inclus** à `j` **exclu** de pas `k`. `i`=*départ*, `j`=*arrivée*, `k`=1 par défaut. Si k est > 0, *départ*=0 et *arrivée*=len(s) | `[1, 2, 3] [1:] == [2, 3]` |
| `len(s)`                 | Retourne la taille (longueur) de la séquence `s`                                                                                                                               | `len( [1, 2, 3] ) == 3`    |
| `min(s)`                 | Retourne le plus petit item de `s`                                                                                                                                             | `min([1, 2, 3]) == 1`      |
| `max(s)`                 | Retourne le plus grand item de `s`                                                                                                                                             | `max([1, 2, 3]) == 3`      |
| s.`index(x [, i [, j]])` | Retourne l'indice de la première occurence de `x` à partir de l'indice `i` et avant `j`. `ValueError` si l'élément n'est pas trouvé. `i`=0, `j`=len(s) par défaut              | `[1, 2, 3].index(2) == 1`  |
| s.`count(x)`             | Retourne le nombre d'occurences de `x`                                                                             | `[1, 2, 3].count(15) == 0` |

##### Opérateurs

| Opérateurs            | Explication                                                                                                                                     | Exemple                  |
| --------------------- |:-----------------------------------------------------------------------------------------------------------------------------------------------:| ------------------------ |
| s `==` t              | **Compare** l'égalité de type, puis de taille, puis de valeurs de deux séquences                                                                | `((1,) == [1]) == False` |
| s `!=` t              | **Compare** l'inégalité de type, puis de taille, puis de valeurs de deux séquences                                                              | `((1,) != [1]) == True`  |
| s `+` t               | Retourne la concaténation de deux séquences **de même type**. Ne marche pas pour `range`. **Il ne faut pas concaténer des séquences immuables** | `[1] + [3] == [1, 3]`    |
| s `* n`               | Retourne `n` références d'une séquence. `n` est un entier. S'il est négatif, il est traité comme 0. Ne marche pas pour `range`                  | `(1,) * 3 == (1, 1, 1)`  |
Les opérateurs de comparaison `<`, `<=`, `>`, `>=`
ne s'appliquent que sur les séquences **de même type**
et utilisent l'[**ordre lexicographique**](#ordre-lexicographique)

#### Muable - `list`

#### Immuable - `tuple`

#### Suite de nombres immuable - `range`

#### Chaine de caractères immuable - `str`

##### Ordre lexicographique
- le même ordre que le premier élément inégal :
`[1, 5] > [1, 2, 8]` car `5 != 2`, donc on utilise l'ordre `5 > 2`
- si l'élément n'existe pas, la séquence la plus courte est ordonnée avant
`[1, 2] < [1, 2, 3]`
- `'0' < '9' < 'A' < 'Z' < 'a' < 'z' < 'À' < 'Ý' < 'à' < 'ÿ'`

##### String formatting

### Collection
#### Données arbitraires - `dict`

#### Données uniques muable - `set`

#### Données uniques immuable - `frozenset`

### Autres types natifs
#### Fonctions

#### Type

##### None

#### Booléens - `True` `False`


## Opérateurs

### `bool`

#### `not`

### `is`


## Fonctions natives

### `all`

### `any`

### `bool`
Voir [`bool`](#bool)
