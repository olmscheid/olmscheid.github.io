---
layout: page
title: Depth First Search
permalink: /learning/dfs/
---

**Learning Objectives**

-	Understand and explain what a depth first search means in the context of graph theory and what some of the use cases are
-	Understand and explain the time complexity of a DFS algorithm
-	Ability to implement a simple DFS algorithm


-Plain Language Definition – A depth first search is an algorithm that allows us to answer two questions:
-	Is there a path from one node to another
-	What is the shortest path between them


Depth First Search will travel a graph as far as it can go along each branch before backtracking. What this means is that unlike Breadth First Search, the algorithm does not explore all neighbors at the current depth before moving on. The way that it does this is by storing nodes that it has discovered in a stack (or using recursion) and following that stack until it finally either reaches what it is looking for or has explored the entire graph. When thinking about a Depth First Search (DFS) algorithm, we'll use our previous dungeon crawler analogy that we saw in the BFS Learning Series Post.


**The Adventurous Dungeon Crawler**


You're the brother of the dungeon crawler adventurer from the BFS post. You, however, are a bit more adventurous and want to explore the cave as far as you can go before backtracking. You want to explore the cave from closest to the entrance to farthest from the entrance, but you want to go as far as you can down each path before backtracking. You do this by exploring rooms in the order that you discover them. If you walk into the cave and there are 3 rooms, you explore room #1 first. If there are more rooms that branch out from room #1, you explore those rooms first before backtracking and exploring room #2 and repeating. After you explore Room #2 and #3, you would then begin exploring the rooms that branched out from Room #1, adding to the list of rooms you explore but following the order of discovery.



![DFS Order](/images/DFS_Order.jpg)




**DFS Implementation**

```
def dfs_recursive_path(g: Graph, ind: int, seen: list, last: list):
    seen[ind] = True
    current: Node = g.nodes[ind]

    for edge in current.get_edge_list():
        neighbor: int = edge.to_node
        if not seen[neighbor]:
            last[neighbor] = ind
            dfs_recursive_path(g, neighbor, seen, last)

def depth_first_search_path(g: Graph) -> list:
    seen: list = [False] * g.num_nodes
    last: list = [-1] * g.num_nodes

    for ind in range(g.num_nodes):
        if not seen[ind]:
            dfs_recursive_path(g, ind, seen, last)

    return last
```

Code Source:  Graph Algorithms The Fun Way by Jeremy Kubica

**Time Complexity**

DFS has a time complexity of O(V + E) where V is the number of vertices and E is the number of edges in the graph. This is because each vertex and edge will be explored at most once during the search process.
