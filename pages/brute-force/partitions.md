# Brute Force: Partitions

Misato es un sport programmer persistente. Esta en medio de una competencia,
quedan pocos minutos y lee un último problema que en resumen es así: 

***Dado un grafo con 1 <= n <= 40 nodos (posiblemente completo). hallar el
 cardinal del [máximo conjunto independiente](https://en.wikipedia.org/wiki/Maximal_independent_set).***


![MIS](https://upload.wikimedia.org/wikipedia/commons/b/b6/Cube-maximal-independence.svg)

Misato ha estudiado recientemente teoría de grafos, se siente algo confiado,
en una primera impresión descarta la idea de una solución por brute force.

> **Misato** (a si mismo): *Como n es menor o igual a 40, una solución O(2\*\*n) es
claramente intratable, asi mismo, es posible hasta un O(n\*\*5). Tal vez la 
ruta sea algo de [flujos en redes](https://en.wikipedia.org/wiki/Flow_network).*

Misato se decide por intentar una solución por esta vía, busca su plantilla del
[algoritmo de Dinic](https://en.wikipedia.org/wiki/Dinic%27s_algorithm) (un algoritmo realmente difícil de implementar). Se pone 
algunos ejemplos usando árboles y grafos bipartitos. Todo cuadra bien...

> **Misado** (a si mismo): *he probado con algunos ejemplos a mano, parece
que halla la respuesta correctamente, intentare mandar.*

Misato decide mandar su solucion, sabe que ha perdido bastante tiempo, lo
suficiente como para no abandonar la idea, pero, sin embargo, recibe un ineludible 
**wrong answer**, vuelve a verificar algunos casos a mano, logra armar
un caso con una respuesta incorrecta de parte de su algoritmo, le cuesta
reaccionar, ha perdido mucho tiempo. Pero inexorablemente el tiempo cae...

Misato termina el contest un poco aturdido. Misato pensaba, y no estuvo del
todo equivocado, que tenia una respuesta correcta. Mira la tabla de posiciones
y puede observar que el problema tiene una cantidad de submisiones correctas
considerablemente mayor a algunos otros problemas que el consideraba 
difíciles. Además, tiene un amigo con un **accepted**, lo busca y no tarda
mucho en encontrarlo, intercambia unas cuantas palabras y mete a colación
el problema en cuestión. Su amigo, sin ningún reparo, le dice:

> **Amigo de Misato**: *"pense que conocias el problema, era un 
[NP complete][3], asi que pense la primera solucion brute-force, no 
demore mucho en ver que la complejidad y pasaba..."*

Misato, entendio, la solución no era tan complicada. Al no conocer un problema
clásico de fuerza bruta, desecho en su primera impresión una idea valida.

##### solution:
```cpp
typedef long long llong;
int MIS(llong nodes, vector<llong> neighboorhood) {
	if(nodes == 0) return 0; //sin nodos
	int node = 63 - __builting_clzll(nodes & -nodes); //nodo con menor id
	return max(
		1 + MIS(~neighboorhood[node] & graph), //tomar nodo (& neighboors? of course...).
		MIS(~node & graph) //no take node. 
	);
}

int solve(vector<vector<int>> Adj) {
	int ord = Adj.size(); //order(Adjacent(G))
	llong graph = (1ll<<ord) - 1; //all nodes
	vector<llong> neighboorhood(ord); //close neighboors set (even the node)
	for (int u = 0; u < Adj.size(); ++u) {
		neighboorhood[u] = 1ll<<u;
		for (int v : Adj[u]) {
			neighboorhood[u] |= 1ll<<v;
		}
	}
	return MIS(graph, neighboorhood);
}
```

Primero veamos la correctitud de la solucion. 


[3]: https://en.wikipedia.org/wiki/NP-completeness