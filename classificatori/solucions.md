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
  <summary><b>Codi alternatiu (Python3)</b></summary>

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

## [Problema C3. Loteria](https://jutge.org/problems/P46281) <a name="C3"/>

Donats dos nombres de 5 dígits, per una banda hem de comprovar si són nombres consecutius i, per altra, quants dígits finals tenen en comú. La primera d'aquestes tasques és més fàcil de fer quan llegim els nombres com a enters (tipus `int`), mentre que la segona és més fàcil si llegim els nombres com a cadenes (tipus `string`). Així doncs, la dificultat del problema radicava en saber convertir bé entre aquests dos formats (o en saber comprovar una de les dues condicions utilitzant el format menys adient). 

A C++, podem passar d'un enter a una string amb la funció `std::to_string`, i d'una string a un enter amb la funció `std::stoi`. Ara bé, cal tenir en compte que si llegim el nombre com un enter i després utilitzem la funció `to_string`, se'ns descarten els zeros inicials que pugui tenir. Aleshores, és més senzill llegir el nombre com una string i després convertir-lo a enter quan faci falta.

<details>
<summary><b>Codi (C++)</b></summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {           
    string x, y;
    int n;
    while(cin >> x >> y >> n) {
        int premi = 0;
        if((stoi(x) + 1) % 100000 == stoi(y) or (stoi(y) + 1) % 100000 == stoi(x))
            premi = 2000; // anterior o seguent
        else {
            vector<int> const premis = {200000, 1000, 250, 35, 10};
            for(int i = 4; i >= 0 and x[i] == y[i]; --i)
                premi = premis[i];
        }
        if(premi) 
            cout << "Heu obtingut un premi de " << premi*n << " euros!" << endl; 
        else
            cout << "Aquest cop no heu tingut sort..." << endl;
    }
}
```
</details>

Per comprovar si els dos nombres són consecutius utilitzem `(x + 1) % 100000 == y or (y + 1) % 100000 == x`. Durant el concurs, diversos participants intentaven comprovar aquesta condició amb fórmules com `(x + 1) % 100000 == y or (x - 1) % 100000 == y`. El problema d'això és que quan prenem el mòdul d'un nombre negatiu, C++ retorna un nombre negatiu. Així doncs, si $x = 0$ i $y = 99999$, la condició `(x - 1) % 100000 == y` s'avaluarà com a `false`, ja que $(0 - 1) \hspace{0.1cm} \\\% \hspace{0.1cm} 100000 = -1 \neq 99999$.

També era possible treballar només amb enters. Aleshores, per trobar quants dígits finals tenen en comú, comprovem primer si l'últim dígit és igual (fent `x % 10 == y % 10`) i, en cas que ho sigui, eliminem l'últim dígit (fent `x /= 10` i `y /= 10`). Ens quedaria el següent codi:

<details>
<summary><b>Codi alternatiu(C++)</b></summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {           
    int x, y, n;
    while(cin >> x >> y >> n) {
        int premi = 0;
        if((x + 1) % 100000 == y or (y + 1) % 100000 == x)
            premi = 2000; // anterior o seguent
        else {
            vector<int> const premis = {10, 35, 250, 1000, 200000};
            for(int i = 0; i < 5; ++i) {
                if(x%10 != y%10)
                    break;
                premi = premis[i];
                x /= 10;
                y /= 10;
            } 
        }
        if(premi) 
            cout << "Heu obtingut un premi de " << premi*n << " euros!" << endl; 
        else
            cout << "Aquest cop no heu tingut sort..." << endl;
    }
}
```
</details>

En Python el procediment anterior quedaria de la manera següent:

<details>
  <summary><b>Codi (Python3)</b></summary>

```py
from yogi import scan

x = scan(int)
while x is not None:
  y, n = scan(int), scan(int)
  premi = 0
  if (x + 1) % 100000 == y or (y + 1) % 100000 == x:
    premi = 2000
  else:
    premis = [10, 35, 250, 1000, 200000]
    for i in range(5):
      if x % 10 != y % 10:
        break
      premi = premis[i]
      x //= 10
      y //= 10
  print("Heu obtingut un premi de " + str(premi*n) + " euros!" if premi else "Aquest cop no heu tingut sort...")
  x = scan(int)
```
</details>

Per als que teniu coneixements més avançats de Python, hi ha maneres més concises de calcular quants dígits finals coincideixen, com per exemple:
```py
premis = [200000, 1000, 250, 35, 10, 0]
premi = next(premis[i] for i in range(6) if x[i:] == y[i:])
```
on estem suposant que `x` i `y` són de tipus `string`.

## [Problema C4. Festival](https://jutge.org/problems/P73935) <a name="C4"/>

<details>
<summary><b>Codi (C++)</b></summary>

```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
  int n;
  while(cin >> n) {
    vector<pair<int,int>> v;
    for(int i = 0; i < n; ++i) {
      int c, a;
      cin >> c >> a;
      v.push_back({c, 0});
      v.push_back({a, 1});
    }
    sort(v.begin(), v.end());
    int maxim = 0;
    int actual = 0;
    for(int i = 0; i < 2*n; ++i) {
      if(v[i].second)
        --actual;
      else {
        ++actual;
        maxim = max(maxim, actual);
      }
    }
    cout << maxim << endl;
  } 
}
```
</details>


<details>
  <summary><b>Codi (Python3)</b></summary>

```py
from yogi import scan

n = scan(int)
while n is not None:
  a = sorted([(scan(int), x) for _ in range(n) for x in range(2)])
  maxim = actual = 0
  for (_, y) in a:
    actual += 1 if y == 0 else -1
    maxim = max(maxim, actual)
  print(maxim)
  n = scan(int)
```
</details>

## [Problema C5. Parell o senar?](https://jutge.org/problems/66510) <a name="C5"/>

<details>
<summary><b>Codi (C++)</b></summary>

```cpp

```
</details>


<details>
  <summary><b>Codi (Python3)</b></summary>

```py

```
</details>

## [Problema C6. Un cicle](https://jutge.org/problems/P20960) <a name="C6"/>

<details>
<summary><b>Codi (C++)</b></summary>

```cpp

```
</details>


<details>
  <summary><b>Codi (Python3)</b></summary>

```py

```
</details>

## [Problema C7. Arbres diferents](https://jutge.org/problems/P20665) <a name="C7"/>

<details>
<summary><b>Codi (C++)</b></summary>

```cpp

```
</details>


<details>
  <summary><b>Codi (Python3)</b></summary>

```py

```
</details>

## [Problema C8. Esperit nadalenc](https://jutge.org/problems/P19910) <a name="C8"/>

<details>
<summary><b>Codi (C++)</b></summary>

```cpp

```
</details>


<details>
  <summary><b>Codi (Python3)</b></summary>

```py

```
</details>