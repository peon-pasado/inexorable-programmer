### Operaciones en espacios vectoriales

```cpp
//implementacion basica

template<class T>
struct Point {
	T x, y;
	Point(T x=0, T y=0): x(x),y(y) {}
	Point operator +(Point other) {return Point(x+other.x, y+other.y);}
	Point operator -(Point other) {return Point(x-other.x, y-other.y);}
	T operator *(Point other) {return x*other.x + y*other.y;}
	T operator ^(Point other) {return x*other.y - y*other.x;}
	Point operator *(int k) {return Point(k * x, k * y);}
	bool operator <(Point other) {return x<other.x or x==other.x and y<other.y;}
	bool operator ==(Point other) {return x==other.x and y==other.y;}
	bool operator <=(Point other) {return *this<other or *this==other;}
	bool operator >(Point other) {return other<*this;}
	bool operator >=(Point other) {return other<=*this;}
	double angle() {return atan2(y, x);}
	Point perp() {return Point(-y, x);}
	Point perp(Point O) {return O + (*this - O).perp();}
};

```

# lecturas recomendadas:

	- [points and vectors][2]
	- [hoffman and kunze (linear algebra)][1] 
	- [Computational geometry in C][3]

[1]: http://www.math.pku.edu.cn/teachers/anjp/textbook.pdf
[2]: http://geomalgorithms.com/points_and_vectors.html
[3]: http://booksdescr.org/ads.php?md5=150E4E29E2844C9F1569D031C85091A7
