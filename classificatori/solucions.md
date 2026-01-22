# Solucions Classificatori oiCat 2026

## Taula de continguts
* [Problema C1. Tres nombres](#C1)
* [Problema C2. Renumeració de cases](#C2)
* [Problema Q1. Nombres reordenables](#Q1)
* [Problema G1. Un dibuix fàcil](#G1)
* [Problema C3. Loteria](#C3)
* [Problema C4. Festival](#C4)
* [Problema Q2. Permutacions sense primers](#Q2)
* [Problema C5. Parell o senar?](#C5)
* [Problema G2. Barrejant colors](#G2)
* [Problema C6. Un cicle](#C6)
* [Problema C7. Arbres diferents](#C7)
* [Problema C8. Esperit nadalenc](#C8)


## [Problema C1. Tres nombres](https://jutge.org/problems/P53899) <a name="C1"/>

Donats tres nombres enters $x$, $y$ i $z$, hem de trobar si hi ha un subconjunt d'ells tals que la suma és múltiple de 4. Com que només hi ha 7 sumes possibles ($x$, $y$, $z$, $x+y$, $x+z$, $y+z$, $x+y+z$), podem comprovar per cada una d'elles si la condició es compleix.

A continuació teniu un codi en C++:

<details>
<summary><b>Codi (C++)</b></summary>

```cpp
#include<bits/stdc++.h>
using namespace std;

bool Val(int x) {
  return x % 4 == 0;
}

int main() {
  int x, y, z;
  cin >> x >> y >> z;
  if(Val(x) or Val(y) or Val(z) or Val(x + y) or Val(x + z) or Val(y + z) or Val(x + y + z))
    cout << "si" << endl;
  else
    cout << "no" << endl; 
}
```
</details>

I una versió equivalent en Python:

<details>
  <summary><b>Codi (Python3)</b></summary>

```py
from yogi import scan

def Val(x):
  return x % 4 == 0

x, y, z = scan(int), scan(int), scan(int)
if Val(x) or Val(y) or Val(z) or Val(x+y) or Val(x+z) or Val(y+z) or Val(x+y+z):
  print("si")
else:
  print("no")
```
</details>

Per a ser més concisos, podem aprofitar la funció `map(f, a)`, que aplica la funció `f` sobre tots els elements de la llista `a`:
<details>
  <summary><b>Codi 2 (Python3)</b></summary>

```py
from yogi import scan

x, y, z = scan(int), scan(int), scan(int)
sumes = [x, y, z, x + y, x + z, y + z, x + y + z]
print("si" if any(map(lambda x : x%4 == 0, sumes)) else "no")
```
</details>
