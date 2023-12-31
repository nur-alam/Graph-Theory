# Graph Theory

## Konigsberg 7 Bridge Problem

<img src="/img/konigsberg7bridge.png" >

Here is the one example of traversal but still one bridge left to visit.
<img src="/img/konigsberg7bridgeTraversal.png">
## Euler Path
Euler Path is a path in a graph that visits all edges and every edge exactly once.
## Euler Path in Undirected Graph

Euler path possible when,
- Every vertices have even degree.
- No odd vertices or exactly two odd vertices and all other vertices have even degree.

**Notes:** If there is odd degree vertex then start traversal from odd degree vertex.

In bellow graph Euler Path possible. There are vertices that have odd degree but exactly two vertext have odd degree.

<img src="/img/eulerPathInUndirecredGraph.png">

Bellow graph Euler Path not possible cause Vertex A, B, C, D have odd degree.

<img src="/img/undirecrtedNotEulerPath.png">


## Euler Path in Directed Graph
Euler path possible when,
- All vertices with nonzero degree belong to a single strongly connected component. 
- In degree is equal to the out degree for every vertex.

<img src="/img/direcrtedEuler.png">

# Graph Data Stucture

A graph data structure is a collection of nodes that have data and are connected to other nodes.

# Types of graph

## Simple Graph

<img src="img/simgleGraph.png" >

## Directed Graph

<img src="/img/directedGraph.png" >

## Undirected Graph

<img src="img/simgleGraph.png" >
## Weighted Graph
<img src="img/WeightedGraph.png" >
## Cyclic Graph
<img src="img/cyclicGraph.png" >
## Acyclic Graph
<img src="img/acyclicGraph.png" >
## DAG(Directed Acyclic Graph)
<img src="img/Dag.png" >

## Handshaking Theorem

### Degree

Degree of a vertex of a graph is the number of edges that are incident to the vertex.

### Indegree of a Graph

Indegree of vertex V is the number of edges which are coming into the vertex V.

### Outdegree of a Graph

Outdegree of vertex V is the number of edges which are going out from the vertex V.

Total degree of a graph is equal to twice of the number of edges.
Total degree of a graph = 2E

$\sum deg(g)$ = 2E

# Graph Representation

## Adjacency Matrix

<img src="/img/adjacency-matrix_1.webp" >

## Adjacency Matrix Code

```
function multiDarray(row, col) {
    return [...Array(row)].map(() => Array(col).fill(0));
}

function main() {
    let [N, E] = readLine().split(' ').map(Number);
    let adjMat = multiDarray(N, N);
    for (let i = 0; i < E; i++) {
        let [u, v] = readLine().split(' ').map(Number);
        adjMat[u][v] = 1;
        adjMat[v][u] = 1;
    }
    console.log(adjMat);
}
```

## Adjacency List

<img src="/img/adjacency-list.webp" >

## Adjacency List Code

```
function main() {
    let [N, E] = readLine().split(' ').map(Number);
    let adjList = [...Array(N)].map(() => new Array());
    for (let i = 0; i < E; i++) {
        let [u, v] = readLine().split(' ').map(Number);
        adjList[u].push(v);
        adjList[v].push(u);
    }
    console.log(adjList);
}
```

<!-- ## Incidence Matrix

<img src="/img/IncidenceMatrix.png" > -->

## Adjacency List Bfs

```
let level = [];
let parent = [];

function getPath(node) {
    let path = [];
    path.push(node);
    while (parent[node] !== -1) {
        node = parent[node];
        path.unshift(node);
    }
    console.log(path);
}

function bfs(adjList, startNode = 0, N) {
    const visited = [...Array(N)].fill(0);
    const q = [];
    const bfsTraversal = [];
    visited[startNode] = 1;
    q.push(startNode);
    parent[startNode] = -1;
    while (q.length) {
        const currentNode = q.shift();
        bfsTraversal.push(currentNode);
        for (let child of adjList[currentNode]) {
            if (!visited[child]) {
                q.push(child);
                visited[child] = 1;
                parent[child] = currentNode;
                level[child] = level[child] + 1;
            }
        }
    }
    console.log('bfsTraversal ', bfsTraversal);
}

function main() {
    const [N, E] = readLine().split(' ').map(Number);
    const adjList = [...Array(N)].map(() => new Array());
    level = [...Array(N)].fill(0);
    parent = [...Array(N)].fill(0);
    for (let i = 0; i < E; i++) {
        const [u, v] = readLine().split(' ').map(Number);
        adjList[u].push(v);
        adjList[v].push(u);
    }
    console.log(adjList);
    bfs(adjList, 0, N);
    getPath(3);
}
```

## Adjacency List Dfs

```
let visited = [];
let dfsTraversal = [];

function dfs(adjList, startNode = 0) {
    visited[startNode] = 1;
    dfsTraversal.push(startNode);
    for (let child of adjList[startNode]) {
        if (!visited[child]) {
            dfs(adjList, child);
        }
    }
}

function main() {
    const [N, E] = readLine().split(' ').map(Number);
    visited = [...Array(N)].fill(0);
    const adjList = [...Array(N)].map(() => new Array());
    for (let i = 0; i < E; i++) {
        const [u, v] = readLine().split(' ').map(Number);
        adjList[u].push(v);
        adjList[v].push(u);
    }
    console.log(adjList);
    dfs(adjList, 0);
    console.log('dfsTraversal ', dfsTraversal);
}

// example 1
// 5 4
// 0 1
// 0 2
// 0 3
// 2 4
// output
// dfs traversal  [ 0, 1, 2, 4, 3 ]

// example 2
// 4 4
// 0 1
// 0 3
// 1 2
// 2 3
// output
// dfs traversal  [ 0, 1, 2, 3 ]
```
