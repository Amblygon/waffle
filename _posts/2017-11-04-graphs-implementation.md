---
layout: post
title: Graph implementation in the two possible ways
categories: graphs
---

{{ page.title }}
================

Adjacency list and Adjacency matrix implementation of Graphs. The choice of the graph representation is situation specific and totally depends on the type of operations to be performed and ease of use.

Adjacency martix implementation
-------------------------------

Know you know how that is. Just in case, a[i][j] = 1 shows there's a edge between i and j nodes. Remember to change the MAX to the required number.

~~~~
bool A[MAX][MAX];

void initialize() {
    for(int i = 0;i < MAX;++i)
        for(int j = 0;j < MAX;++j)
            A[i][j] = false;
}

// Code for Main function

    int x, y, nodes, edges;
    initialize();       
    cin >> nodes;       
    cin >> edges;
    for(int i = 0;i < edges;++i) {
        cin >> x >> y;
        A[x][y] = true;
    }
    
~~~~

Removing an edge takes O(1) time in this implementation. Queries like whether there is an edge from vertex ‘u’ to vertex ‘v’ are efficient and can be done O(1). Heavy memory utilisation. 

Adjacency list implemenation
----------------------------

V in the function call represents the number of nodes - remember to change the placeholder to the required value or input. Don''t forget to account of the fact that the given graph deals entirely from index 0. Code for Adjacency list implementation taken from [GeeksforGeeks](http://www.geeksforgeeks.org/graph-and-its-representations/), presented with minor modifications and simplifications. 

~~~~
struct AdjListNode {
    int dest;
    struct AdjListNode* next;
};

struct AdjList {
    struct AdjListNode *head;
};

struct Graph {
    int V;
    struct AdjList* array;
};
 
struct AdjListNode* newAdjListNode(int dest) {
    struct AdjListNode* newNode = (struct AdjListNode*) malloc(sizeof(struct AdjListNode));
    newNode->dest = dest;
    newNode->next = NULL;
    return newNode;
}
 
struct Graph* createGraph(int V) {
    struct Graph* graph = (struct Graph*) malloc(sizeof(struct Graph));
    graph->V = V;
 
    graph->array = (struct AdjList*) malloc(V * sizeof(struct AdjList));
    
    int i;
    for (i = 0; i < V; ++i)
        graph->array[i].head = NULL;
 
    return graph;
}
 
// Adds an edge to an undirected graph
void addEdge(struct Graph* graph, int src, int dest)
{
    // Add an edge from src to dest.  A new node is added to the adjacency
    // list of src.  The node is added at the begining
    struct AdjListNode* newNode = newAdjListNode(dest);
    newNode->next = graph->array[src].head;
    graph->array[src].head = newNode;
 
    // Since graph is undirected, add an edge from dest to src also
    newNode = newAdjListNode(src);
    newNode->next = graph->array[dest].head;
    graph->array[dest].head = newNode;
}

//Code for main - function calls
    struct Graph* graph = createGraph(V);
    addEdge(graph, a, b)
~~~~
