# EX 5E Minimum Spanning Tree – Borůvka’s Algorithm

## DATE: 10-11-2025

## AIM:

To write a Java program to find the **Minimum Spanning Tree (MST)** of a weighted undirected graph using **Borůvka’s Algorithm**.

---

## Algorithm:

1. Read the number of vertices **V** and edges **E**.
2. Initialize each vertex as its own component using **Disjoint Set Union (DSU)**.
3. While more than one component exists:

   * Create an array `cheapest[]` to store the cheapest edge for each component.
   * For each edge, determine the components of its endpoints using DSU:

     * If they belong to different components, update the cheapest edge for those components.
   * For every component, add the cheapest edge to the MST if it does not form a cycle.
   * Union the components connected by these edges and reduce the component count.
4. Continue until only one component remains.
5. Print all selected MST edges and the total weight.

---

## Program:

```java
/*
Developed by: MASINA SREE KARSH
Register Number: 212223100033
*/

import java.util.*;

public class BoruvkaMST {
    static int[] parent;
    static int[] rank;

    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

    static void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX == rootY) return;

        if (rank[rootX] < rank[rootY])
            parent[rootX] = rootY;
        else if (rank[rootY] < rank[rootX])
            parent[rootY] = rootX;
        else {
            parent[rootY] = rootX;
            rank[rootX]++;
        }
    }

    static int boruvkaMST(int V, List<Edge> edges) {
        parent = new int[V];
        rank = new int[V];
        int numTrees = V;
        int MSTweight = 0;

        for (int v = 0; v < V; v++) {
            parent[v] = v;
            rank[v] = 0;
        }

        while (numTrees > 1) {
            Edge[] cheapest = new Edge[V];

            for (Edge e : edges) {
                int set1 = find(e.src);
                int set2 = find(e.dest);

                if (set1 == set2) continue;

                if (cheapest[set1] == null || e.weight < cheapest[set1].weight)
                    cheapest[set1] = e;

                if (cheapest[set2] == null || e.weight < cheapest[set2].weight)
                    cheapest[set2] = e;
            }

            for (int i = 0; i < V; i++) {
                Edge e = cheapest[i];
                if (e != null) {
                    int set1 = find(e.src);
                    int set2 = find(e.dest);

                    if (set1 == set2) continue;

                    MSTweight += e.weight;
                    System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
                    union(set1, set2);
                    numTrees--;
                }
            }
        }

        return MSTweight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        int totalWeight = boruvkaMST(V, edges);
        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        src = s;
        dest = d;
        weight = w;
    }
}
```

---

## Output (Example):

<img width="869" height="540" alt="image" src="https://github.com/user-attachments/assets/7a8fe68f-2ec5-4cf9-89d4-189851fafc23" />


---

## Result:

The program was successfully implemented using **Borůvka’s Algorithm**, and the expected output was verified.
