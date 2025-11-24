# EX 5C Graph Coloring

## DATE: 2-11-2025

## AIM:

To write a Java program to determine whether N radio towers can be assigned at most M frequency channels such that no two adjacent towers share the same channel, using the **Graph Coloring (Backtracking)** approach.

---

## Algorithm:

1. Read inputs: number of towers **N**, number of channels **M**, and number of edges **E**.
2. Build an adjacency list to represent the undirected graph of tower communication range.
3. Maintain a `color[]` array of size `N` initialized to 0 (uncolored).
4. Use a **recursive backtracking function**:

   * For each tower, try assigning a channel `1` to `M`.
   * Before assigning, check using `isSafe()` that no adjacent tower has the same color.
5. If assigning a color leads to a valid configuration for all towers → return **true**.
6. If no color can be assigned for a tower → backtrack and try another color.
7. If no assignment is possible → print **"NO"**, otherwise **"YES"**.

---

## Program:

```java
/*
Program to implement Reverse a String
Developed by: MASINA SREE KARSH
Register Number: 212223100033
*/

import java.util.*;

public class RadioTowerChannelAssignment {

    private static boolean isSafe(List<List<Integer>> graph, int node, int[] color, int c) {
        for (int neighbor : graph.get(node)) {
            if (color[neighbor] == c)
                return false;
        }
        return true;
    }

    public static boolean isColorable(List<List<Integer>> graph, int[] color, int node, int m, int n) {
        if (node == n)
            return true;

        for (int c = 1; c <= m; c++) {
            if (isSafe(graph, node, color, c)) {
                color[node] = c;

                if (isColorable(graph, color, node + 1, m, n))
                    return true;

                color[node] = 0;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int e = sc.nextInt();

        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++)
            graph.add(new ArrayList<>());

        for (int i = 0; i < e; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int[] color = new int[n];

        if (isColorable(graph, color, 0, m, n))
            System.out.println("YES");
        else
            System.out.println("NO");

        sc.close();
    }
}
```

---

## Output:

<img width="931" height="549" alt="image" src="https://github.com/user-attachments/assets/fdced9d4-60e9-4db6-a69c-b2cbf53acb7d" />


---

## Result:

The program was successfully implemented using the **Graph Coloring Backtracking** method and the expected output was verified.
