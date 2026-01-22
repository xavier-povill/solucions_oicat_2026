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

<details>
  <summary><b>Repte</b></summary>
  Suposeu que en lloc de 3 tenim $100.000$ joguines diferents. Com resoldríeu aleshores el problema?
</details>


## [Problema C2. Renumeració de cases](https://jutge.org/problems/P90007) <a name="C2"/>

Les cases amb número parell passen de tenir números $(2, 4, 6, 8, \dots)$ a $(-1, -2, -3, -4, \dots)$ . Això ho podem expressar algebraicament com que la casa amb número $x$ passa a tenir el número $-x/2$.

Per altra banda, les cases amb número senar passen de tenir números $(1, 3, 5, 7, \dots)$ a $(1, 2, 3, 4, \dots)$ . És a dir, la casa amb número $x$ passa a tenir el número $(x + 1)/2$.

Així doncs, per resoldre el problema, comprovem primer si el nombre que ens donen és parell o senar i, depenent d'això, apliquem la fórmula corresponent.

<details>
<summary><b>Codi (C++)</b></summary>

```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
  int x;
  while(cin >> x) {
    if(x % 2 == 0)
      cout << -x/2 << endl;
    else
      cout << (x + 1)/2 << endl;
  } 
}
```
</details>

Observeu que a l'enunciat no ens diuen el nombre de casos que ha de resoldre el nostre programa (el fitxer d'entrada pot tenir moltes línies). Per aquest motiu, a la solució anterior utilitzem l'estructura
```cpp
int x;
while(cin >> x) {
  //...
}
```
que va llegint enters $x$ del fitxer d'entrada fins que arriba al final del fitxer, moment en el qual surt del bucle (internament, això passa perquè la funció `std::cin` retorna un objecte que, si es converteix a tipus `bool`, retorna `false` en cas que l'última lectura hagi fallat - <a href="https://en.cppreference.com/w/cpp/io/basic_ios/operator_bool">vegeu enllaç</a>).

A continuació teniu la versió en Python del mateix codi:

<details>
  <summary><b>Codi (Python3)</b></summary>

```py
from yogi import scan

x = scan(int)
while x is not None:
  if x % 2 == 0:
    print(-x//2)
  else:
    print((x + 1)//2)
  x = scan(int)
```
</details>

Observeu que utilitzem la funció `scan`, de la llibreria `yogi`, per imitar el comportament que té `while(cin >> x)` en C++. Concretament, `scan(int)` retorna o bé un enter, o bé un objecte amb valor `None`, en cas que s'hagi arribat al final del fitxer d'entrada. Així doncs, amb un bucle de la forma
```py
x = scan(int)
while x is not None:
  #...
  x = scan(int)
```
podem llegir tots els enters del fitxer d'entrada, sense que ens doni cap error quan arribem al final del fitxer.