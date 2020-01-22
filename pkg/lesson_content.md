Lesson content flow (potential, 20min altogether)

##Introduction to graphs (10 min Mandy)
#What are graphs?
Graphs are mathematical structures used to model pairwise relations between objects. A graph in this context is made up of vertices (also called nodes or points) which are connected by edges

https://en.wikipedia.org/wiki/Graph_theory

#What kind of problems do graphs sovle?

- Computer networks - Often nodes will represent end-systems or routers, while edges represent connections between these systems.
- Sequence of events - Prioritising projects, finding duration of each project. Use tree structures
- Pathing and Maps: Trying to find shortest or longest paths from some location to a destination makes use of graphs. This can include pathing like you see in an application like Google maps, or calculating paths for AI characters to take in a video game, and many other similar problems.
- Constraint Satisfaction: Find some goal that satisfies a list of constraints. For example,Matching professors to courses so classes don't clash
- Constraint satisfaction problems like this are often modeled and solved using graphs.
- Molecules: Model atoms and molecules for studying their interaction and structure among other things.

#How are graphs used at fromatob?
Our main search functions invovles using an undirected graph to connect cities on a map.
We use open data on public transit timetables and extract the fields we need to build network graphs. Then we create indivudual graphs for each mode of transportation. After that, we run a traversal algorithm like Dijkstra algorithm to find the shortest distance

Smaller things we do with graphs
Eg. Clean up Nodes which are not relevant stations
Eg. Consolidate cluster of stations into one node to speed up search - Alexanderplatz is seen as 10 train stations on a map so we use a cluster algorithm to represent it with a single node

Check out an example of a graph here `pkg/graph_visual.png`

#Explore mini challenges
  Print the Node ID for Berlin
  Print the Nodename for NodeID 7
  Print the nodes connected to Berin

Eg.
  fmt.Println(g.LookupNode("Berlin"))
  fmt.Println(g.NodeName(6))
  fmt.Println(g.Neighbors(0))

  Write forloop to get from Berlin to Leipzig

  var n = g.Neighbors(0)
  var j, _ = g.LookupNode("Leipzig")

  for _, a := range n {
    if a == j {
      fmt.Printf("Connection exists!")
    }


##BFS (10 min Jessica)

Breadth First Search (BFS)- is used to explore the relation between nodes (or vertices) in a graph via the connecting edges. It differs from another fundamental search algorithm, depth first search, in the way that it explores the graph. It explores the neighbour nodes first before moving on to the next level of neighbours because of this BFS is particularly useful for finding the shortest path on unweighted graphs.

So let’s look at what this means and how the algorithm works.

To show the advantage of BFS it can be useful to compare it to [depth first search](https://en.wikipedia.org/wiki/Depth-first_search) (DFS) you may have already come across DFS. Incase you have not, here is a small break down.

We start from a chosen node and arbitrary take a next node going all the way along until we can go no further (to it’s furthest depth) We then backtrack through the graph until we find another path following this new path to it’s end. This pattern of going to a deadend and backtracking continues until we backtrack all the way to the chosen start node. It means we have explore every node in the graph. Worthy of noting is that DFS uses a [stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) to track where it is in the graph. Stacks follow a last in first out data structure.

This is great if we want to know the relationship between nodes but depending on the graph may be more time consuming than we would like. Imagine for instance a very deep graph where the node we are looking for is across from the start node rather than below it. This is where [Breadth first search](https://en.wikipedia.org/wiki/Breadth-first_search) comes in handy! BFS checks all sibling elements before going to the next row of the graph. This can be accomplished using a [Queue](https://en.wikipedia.org/wiki/Queue_(abstract_data_type)). Unlike a stack queues use a first in first out structure. BFS checks whether a node (sometimes called vertex) has been discovered before enqueueing the node rather than delaying this check until the node is dequeued from the queue.

What are Queues?
Step by step on how to queue and visit (screenshot )

Gif of BSF and DSF:

![alt-text](pkg/dfsvsbfs.gif)

Further reading about [DFS versus BFS](https://medium.com/@kenny.hom27/breadth-first-vs-depth-first-tree-traversal-in-javascript-48df2ebfc6d1) and [traversing a graph with BSF](https://medium.com/basecs/going-broad-in-a-graph-bfs-traversal-959bd1a09255)
