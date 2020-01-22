# go-workshop

Welcome to the Women Who Go workshop in January challenge with fromAtoB

## What does fromatob do?

fromAtoB's vision is to combine flights, trains, long distance buses and car-pooling towards your perfect trip from A to B within one booking, one payment, within less than 30 seconds.


## What are we doing today?

1. Brief explanation on graphs at fromAtoB
2. Mini challenge to familiarise ourselves with our graph `pkg/graph.go`
3. Breadth-first-search algorithm
4. Bring in the mission


## 1. What are graphs?

Graphs are mathematical structures used to model pairwise relations between objects. A graph in this context is made up of vertices (also called nodes or points) which are connected by edges

https://en.wikipedia.org/wiki/Graph_theory


### What kind of problems do graphs solve?

Graphs are used for lots of things, but here are some examples:

- Computer networks - Often nodes will represent end-systems or routers, while edges represent connections between these systems.
- Sequence of events - Prioritising projects, finding duration of each project. Use tree structures
- Pathing and Maps: Trying to find shortest or longest paths from some location to a destination makes use of graphs. This can include pathing like you see in an application like Google maps, or calculating paths for AI characters to take in a video game, and many other similar problems.
- Constraint Satisfaction: Find some goal that satisfies a list of constraints. For example, Matching professors to courses so classes don't clash. Constraint satisfaction problems like this are often modeled and solved using graphs.
- Molecules: Model atoms and molecules for studying their interaction and structure among other things.

### How are graphs used at fromAtoB?

Our main search functions involves using an undirected graph to connect cities on a map.
We use open data on public transit timetables and extract the fields we need to build network graphs. Then we create indivudual graphs for each mode of transportation. After that, we run a traversal algorithm like Dijkstra algorithm to find the shortest distance


## 2. Explore mini challenges

The challenges are based on a simplified graph of train connections, which is loaded from `trains.txt`. Take a look at `trains.png` for a graphical view.

- Print the Node ID for Berlin
- Print the Nodename for NodeID 7
- Print the nodes connected to Berin

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
    }

## 3. Breadth First Search Algorithm

We can use various search algorithms to explore the relation between nodes (or vertices) in a graph via the connecting edges. Two of the fundamental ones used for graphs
are [depth first search](https://en.wikipedia.org/wiki/Depth-first_search) and [breadth first search](https://en.wikipedia.org/wiki/Breadth-first_search), for the challenge today we will use the second one but to better undstand it we will compare the two.

Lets start with depth first search. We start from a chosen node and arbitrary take a next node going all the way along until we can go no further (to it’s furthest depth) We then backtrack through the graph until we find another path following this new path to it’s end. This pattern of going to a deadend and backtracking continues until we backtrack all the way to the chosen start node. It means we have explore every node in the graph. Worthy of noting is that DFS uses a [stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) to track where it is in the graph. Stacks follow a last in first out data structure.

This is great if we want to know the relationship between nodes but depending on the graph may be more time consuming than we would like. Imagine for instance a very deep graph where the node we are looking for is across from the start node rather than below it. This is where breadth first search comes in handy as it explores the graph in a different manner! BFS checks all sibling elements before going to the next row of the graph - hence it being called breadth first. This makes BFS particularly useful for finding the shortest path on unweighted graphs.

BFS is accomplished using a [Queue](https://en.wikipedia.org/wiki/Queue_(abstract_data_type)). Unlike a stack queues use a first in first out structure. BFS checks whether a node (sometimes called vertex) has been discovered (visited) before enqueueing (adding) the node to the queue rather than delaying this check until the node is dequeued (removed) from the queue. We will implement the queue here [here](/pkg/queue.go)

This gif shows how both BFS and DFS check through the graph:

![alt-text](/dfsvsbfs.gif)

#### Further reading

- [DFS versus BFS](https://medium.com/@kenny.hom27/breadth-first-vs-depth-first-tree-traversal-in-javascript-48df2ebfc6d1)
- [Traversing a graph with BFS](https://medium.com/basecs/going-broad-in-a-graph-bfs-traversal-959bd1a09255)

## 4. The mission

Part 1 - Connected or not?

Use the `Graph` structure to find out if cities a and b are connected or not
Tips on how to start:
- In `pkg/algorithms.go` fill in the `Connected` function so it returns true
- Try running `go run cmd/go-workshop/main.go` to see the Graph structure. If your algorthm works, it should print “ok” on each line.
- There's a `Queue` type in `pkg/queue.go` which will be useful if you decide to implement BFS.

Part 2 - Shortest path

Well done on completing part 1! Now that you know if cities a to b are connected or not, let's find the shortest path (shortest number of steps in between)
Tips on how to start:
- Fill in the ShortestPath function in `pkg/algorithms.go`
- A path is represented by a slice of int with the node IDs. For example, a path from node 4 to node 6 and then to node 2 would be represented by `[]int{4, 6, 2}`


## Bonus mission

If you've completed the mission and you're getting bored of graph algorithms, let's look at graph data structures instead!

There's more than one way to store the edges in a graph. The one in `pkg/graph.go` uses an “adjacency list,” which means for each node it stores a list of its neighbors -- that's the `edges` field in the struct.

Another way is to create a 2-D matrix of booleans. The boolean in row i, column j of the matrix will be true if there's an edge from node i to node j, otherwise it'll be false. This is called an “adjacency matrix.”

Try to change the Graph to use an adjacency matrix instead of an adjacency list! Do it in a way that the code you wrote in `pkg/algorithms.go` still works -- the methods that access the Graph should work as before.

However, if you want to change the way the graph is *created*, go ahead! You'll just need to adapt the `LoadGraph` function in `pkg/files.go`.
