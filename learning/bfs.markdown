---
layout: page
title: Breadth First Search
permalink: /learning/bfs/

---

**Learning Objectives**

-	Understand and explain what a breadth first search means in the context of graph theory and what some of the use cases are
-	Understand and explain the time complexity of a BFS algorithm
-	Ability to implement a simple BFS algorithm


Plain Language Definition – A breadth first search is an algorithm that allows us to answer two questions:
-	Is there a path from one node to another
-	What is the shortest path between them


Breadth First Search will travel a graph one layer at a time, exploring on a “first come first serve basis”. What this means is that unlike Depth First Search, the algorithm does not travel as far as it can go immediately. The way that it does this is storing nodes that it has discovered in a queue and following that queue in order until it finally either reaches what it is looking for or has explored the entire graph.
When thinking about a Breadth First Search (BFS) algorithm, I ran across two very helpful analogies.


**The Methodical Dungeon Crawler**


The first example is to pretend you’re an adventurer who has discovered a new cave consisting of many different connected rooms. You want to methodically map out the dungeon so that you explore the cave from closest to the entrance to farthest from the entrance. You don’t want to venture too far with unexplored rooms behind you. You do this by exploring rooms in the order that you discover them. If you walk into the cave and there are 3 rooms, you explore room #1 first. If there are more rooms that branch out from room #1, you put those on your list to explore but first backtrack and explore room #2 and repeat. After you explore Room #2 and #3, you would then begin exploring the rooms that branched out from Room #1, adding to the list of rooms you explore but following the order of discovery.



![BFS Order](/images/BFS_Order.jpg)


**Degrees of Separation**


The second example is that you want to find someone in your personal network who has a particular item that you want to buy (let’s say an old SNES video game system). You would prefer to buy from the first person who is closest in your network. That means direct friends (1st degree) first, friends of friends (2nd degree) next, and so on until you find someone who has what you’re looking for. You want to ask everyone in each degree ring before moving to the next degree.



![Degrees of Separation](/images/BFS_Degrees.jpg)


**BFS Implementation**

```
breadth_first_search(g: Graph, start: int): list:
    seen: list = [False] * g.num_nodes
    last: list = [-1] * g.num_nodes
    pending: queue.Queue = queue.Queue()
    pending.put(start)
    seen[start] = True

    while not pending.empty():
        index: int = pending.get()
        current: Node = g.nodes[index]

        for edge in current.eget_edge_list():
            neighbor: int = edge.to_node
            if not seen[neighbor]:
                pending.put(neighbor)
                seen[neighbor] = True
                last[neighbor] = index

    return last
```

Code Source:  Graph Algorithms The Fun Way by Jeremy Kubica



