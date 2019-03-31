# Implementing the operations
1. Find query: check if two objects are in the same component.
2. Union command: Replacce components containing two objects with their union.

# Union-find data type(API)
1. Design efficient data structure for union-find
2. Number of objects N can be huge.
3. Number of operations M can be huge.
4. Find quries and union commands may be intermixed.

```java
public class UF {
    public UF(int N){ // initialize union-find data structure with N objects

    }
    public void union(int p, int q){ // add connection between p nad q

    }
    public boolean connected(int p, int q){ // are p and q in the same component?

    }
    public int find(int p){ // component identifier for p

    }
    public int count(){ // number of components

    }
}
```
# Data structure
1. Integer array id[] of size N
2. Interpretation: p and q are connected iff they have same id.
   
# Quick Find
1. Find: check if p and q have the same id
2. Union: To merge components containing p and q. change all entries whose id quals id[p] to id[q].

# Quick Union
1. Find: Check if p and q have the same root.
2. Union: To merge components containing p and q, set the id of p's root to the id of q's root.