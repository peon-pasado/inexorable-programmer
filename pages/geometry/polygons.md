### poligonos

Los poligonos nos permiten representar muchos objetos reales,
ademas, nos permite simplificar objetos muchos mas complejos
en piezas simples.

Definiremos un poligono como una secuencia ciclica de aristas, 
tal que dos aristas no adjacentes no se intersectan. 

```cpp
template<class T> 
class Polygon : public vector<Point<T>> {
	
};
inline int prev(int i, int n) {return i == 0 ? n-1 : i-1;}
inline int next(int i, int n) {return i == n-1 ? 0 : i+1;}
template<class T> inline int sgn(const T& x) {return (T(0)<x) - (x<T(0));} 
```

#### teorema ([teorema de la curva de jordan][1]):
 
Toda curva simple plana cerrada divide el plano en dos 
componentes.

#### polygon test:

```cpp
template<class T>
friend int Polygon::in(Point<T> p) {
	int n = static_cast<int>(this->size()), windingNumber;

}
```

#### Area de un poligono

```cpp
double area(Polygon p) {
	int n = p.size();
	double res = 0.d;
	for (int i = 0; i < n; ++i) {
		res += p[i] ^ p[(i+1) % n];
	}
	return abs(res) / 2;
}
```



[1]: http://www-cgrl.cs.mcgill.ca/~godfried/teaching/cg-projects/97/Octavian/compgeom.html
[2]: https://codeforces.com/blog/entry/48868















