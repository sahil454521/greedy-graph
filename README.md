# greedy-graph
#include <stdio.h>
#include <stdlib.h>

#define V 5

bool isValid(int v, int graph[V][V], int result[], int color) {
    for (int i = 0; i < v; i++) {
        if (graph[v][i] && result[i] == color) {
            return false;
        }
    }
    return true;
}

bool greedyColoring(int graph[V][V]) {
    int result[V];
    for (int i = 0; i < V; i++) {
        result[i] = -1;
    }

  result[0] = 0;

  for (int u = 1; u < V; u++) {
        for (int i = 0; i < 3; i++) {
            if (isValid(u, graph, result, i)) {
                result[u] = i;
                break;
            }
        }
    }

  int color;
    for (color = 0; color < 3; color++) {
        if (isValid(0, graph, result, color)) {
            break;
        }
    }
    result[0] = color;

   printf("Vertex colors:\n");
    for (int u = 0; u < V; u++) {
        char color;
        if (result[u] == 0) {
            color = 'R';
        } else if (result[u] == 1) {
            color = 'G';
        } else {
            color = 'B';
        }
        printf("Vertex %d -- Color %c\n", u, color);
    }

   return true;
}

int main() {
    int graph[V][V] = {
        {0, 1, 1, 1, 1},
        {1, 0, 1, 0, 0},
        {1, 1, 0, 1, 0},
        {1, 0, 1, 0, 1},
        {1, 0, 0, 1, 0}
    };

   greedyColoring(graph);
    return 0;
}
