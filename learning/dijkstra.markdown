---
layout: page
title: Dijkstra's Algorithm
permalink: /learning/dijkstra/
---

**Learning Objectives**

- Understand and explain what Dijkstra's algorithm means in the context of graph theory and what some of its use cases are
- Understand the role that edge weights and a priority queue play in finding the shortest path
- Understand and explain the time complexity of Dijkstra's algorithm
- Ability to implement a simple version of Dijkstra's algorithm

Plain Language Definition - Dijkstra's algorithm allows us to answer two questions in a weighted graph:

- What is the shortest path from one node to another?
- What is the shortest distance from a starting node to every other reachable node?


Unlike Breadth First Search, Dijkstra's algorithm does not assume that every edge is equal. Each edge has a weight that can represent distance, time, cost, difficulty, or really anything else that can be measured. The algorithm uses those weights to find the path with the lowest total cost.

Dijkstra's algorithm begins at a starting node and assigns it a distance of zero. Every other node begins with a tentative distance of infinity because we have not found a route to it yet. From there, the algorithm always selects the unvisited node with the lowest known distance, checks each of its neighbors, and determines whether traveling through the current node creates a shorter route. This process is called relaxing an edge.

If the new route is shorter, the algorithm updates the neighbor's distance and records the current node as its predecessor. Once the node with the lowest tentative distance is removed from the priority queue, that distance is finalized. The algorithm continues until the priority queue is empty or until it reaches the destination it is looking for.

When thinking about Dijkstra's algorithm, we'll once again return to the dungeon-crawler family from the BFS and DFS Learning Series posts.

**The Calculating Dungeon Crawler**

You're another sibling of the dungeon crawlers from the BFS and DFS posts. Unlike your siblings, you are less concerned with exploring every room in a particular order. You just want to find the least expensive route through the dungeon.

Every hallway has a number posted above it representing how difficult it is to travel through. One hallway might have a cost of two because it is short and clear. Another might have a cost of six because it is full of goblins, tomb bandits, or who knows what. A route with more hallways could still be better if its total cost is lower.

You begin at the dungeon entrance with a total cost of zero. Every room you have not reached yet has a cost of infinity. You look at the available hallways, calculate the total cost required to reach each neighboring room, and write down the cheapest route you currently know about.

You then choose the room with the lowest total cost from the entrance, not necessarily the room connected by the cheapest individual hallway.  Dijkstra's algorithm cares about the total cost of the entire route, not just the weight of the most recent edge.

Each time you reach a room, you check whether it gives you a cheaper route to any neighboring rooms. If it does, you erase the old cost, write down the new one, and record which room you came from. That recorded connection becomes part of the current shortest path. Once you select the lowest cost room from your priority queue, its shortest distance is finalized and you continue the process.

![Dijkstra's Algorithm](/images/dijkstra.jpg)

**Time Complexity**

This implementation of Dijkstra's algorithm has a time complexity of O((V + E) log V), where V is the number of vertices and E is the number of edges in the graph. This is commonly shortened to O(E log V) for a connected graph.