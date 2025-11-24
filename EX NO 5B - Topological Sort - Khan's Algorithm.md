# EX 5B Topological Sort – Kahn's Algorithm

## DATE: 30-11-2025

## AIM:

To write a Java program to find a valid order of task execution using **Topological Sorting (Kahn’s Algorithm)**.
The program should detect if a valid release schedule exists or if cyclic dependencies make scheduling impossible.

---

## Algorithm:

1. Read the number of tasks `n` and dependencies `m`.
2. Create an adjacency list for the directed graph.
3. Create an indegree array to count incoming edges for each task.
4. For each dependency pair `[a, b]`, add edge `b → a` and increase indegree of `a`.
5. Add all tasks with indegree **0** into a queue (tasks with no dependencies).
6. While queue is not empty:

   * Remove a task from the queue → add it to the result list
   * Reduce indegree of its adjacent tasks
   * If any task's indegree becomes 0, add it to the queue
7. If the result list contains all tasks → valid schedule
8. Otherwise, a cycle exists → print **"Release cannot be scheduled"**

---

## Program:

```java
/*
Program to implement Reverse a String
Developed by: MASINA SREE KARSH
Register Number: 212223100033
*/

import java.util.*;

public class prog {

    public static List<Integer> findTaskOrder(int n, int[][] dependencies) {
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < n; i++) adj.add(new ArrayList<>());

        int[] indegree = new int[n];

        for (int[] dep : dependencies) {
            int a = dep[0];
            int b = dep[1];
            adj.get(b).add(a);
            indegree[a]++;
        }

        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) q.add(i);
        }

        List<Integer> order = new ArrayList<>();

        while (!q.isEmpty()) {
            int node = q.poll();
            order.add(node);

            for (int next : adj.get(node)) {
                indegree[next]--;
                if (indegree[next] == 0) q.add(next);
            }
        }

        if (order.size() != n) return null;
        return order;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();

        int[][] dependencies = new int[m][2];
        for (int i = 0; i < m; i++) {
            dependencies[i][0] = sc.nextInt();
            dependencies[i][1] = sc.nextInt();
        }

        List<Integer> result = findTaskOrder(n, dependencies);

        if (result == null) {
            System.out.println("Release cannot be scheduled");
        } else {
            for (int task : result) {
                System.out.print(task + " ");
            }
        }
    }
}
```

---

## Output:

<img width="956" height="550" alt="image" src="https://github.com/user-attachments/assets/8ae1a6b2-acb4-401e-86f7-ea9bf0000a3d" />


---

## Result:

The program was successfully implemented using **Kahn’s Algorithm**, and the output was verified.
