# EX 5D Flower Planting

## DATE: 05-11-2025

## AIM:

To write a Java program to assign one of **four flower types** to each garden such that **no two adjacent gardens have the same flower type**, using a greedy algorithm.
A valid assignment is always guaranteed because no garden has more than 3 neighbours.

---

## Algorithm:

1. Read the number of gardens **n** and number of paths **m**.
2. Build an adjacency list to represent the bidirectional paths between gardens.
3. Create an array `res[]` of size `n` to store the assigned flower types.
4. For each garden:

   * Check all its neighbours and mark the flower types used by those neighbours.
   * Assign the **smallest flower type (1 to 4)** that is not used by its neighbours.
5. Print the resulting flower assignment.
6. Since each garden has at most 3 neighbours, at least one of the four flower types will always be available.

---

## Program:

```java
/*
Program to implement Reverse a String
Developed by: MASINA SREE KARSH
Register Number: 212223100033
*/

import java.util.*;

public class GardenFlowerPlanner {

    public static int[] assignFlowers(int n, int[][] paths) {
        @SuppressWarnings("unchecked")
        List<Integer>[] adj = new ArrayList[n];
        for (int i = 0; i < n; i++) adj[i] = new ArrayList<>();

        for (int[] p : paths) {
            int u = p[0] - 1;
            int v = p[1] - 1;
            adj[u].add(v);
            adj[v].add(u);
        }

        int[] res = new int[n];

        for (int i = 0; i < n; i++) {
            boolean[] used = new boolean[5];

            for (int nei : adj[i]) {
                if (res[nei] != 0)
                    used[res[nei]] = true;
            }

            for (int f = 1; f <= 4; f++) {
                if (!used[f]) {
                    res[i] = f;
                    break;
                }
            }
        }

        return res;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int m = sc.nextInt();

        int[][] paths = new int[m][2];
        for (int i = 0; i < m; i++) {
            paths[i][0] = sc.nextInt();
            paths[i][1] = sc.nextInt();
        }

        int[] result = assignFlowers(n, paths);

        for (int flower : result) {
            System.out.print(flower + " ");
        }
        System.out.println();

        sc.close();
    }
}
```

---

## Output:

<img width="509" height="554" alt="image" src="https://github.com/user-attachments/assets/ec94ee3c-fe5f-4efc-9a20-134d5d094958" />

---

## Result:

The program was successfully implemented using a greedy flower assignment approach, and the expected output was verified.


