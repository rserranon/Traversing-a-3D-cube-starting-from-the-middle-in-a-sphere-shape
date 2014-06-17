Traversing a 3D cube starting from the middle in a sphere shape
===============================================================

The way this works is by creating a graph, where each cell is a node. Since the graph have the shape of a cube, therefore each node must have a link to its X, Y and Z neighbour. The first proceeder to do is creating the graph by feeding the program the relation between neighbour nodes. For instance, we should give the program an input saying that node zero is connected to node one, etc ... After telling the program about how the nodes are connected to form the cube, it's easy to start thinking about traversing this graph. A popular algorithm for traversing graphs is called Breadth First Traversal (BFT), this algorithm allows nodes to be traversed in a distributed way. For example, if you have a tree, which is a type of graphs, traversing it using BFT will print the root first, then prints each level at a time, so it's kind of traversing the tree from the starting point by propagating fairly in all branches. In your example of traversing a cube starting from the middle to the corners is exactly what BFT can do for you. In this case, BFT will start from the middle and start traversing the nodes surface by surface, and since we are starting from the middle point, the propagation will take a sphere shape.


**What is BFT**<br>
BFT needs to use a data structure called Queue which is a First In First Out list. First we offer to the queue the starting point and we mark it as visited, meaning that it has entered the queue and is not allowed to enter any time later in the traversal. Then we will apply a proceeder that will poll the head node, mark it as visited, and offer its unvisited neighbours. The same process is done again and again until all nodes are visited and therefore the queue is empty. The reason we use a queue here is to allow nodes to be traversed in balanced way. In this cube traversal program, offering the middle node will follow by polling it out from the queue and offering its 6 neighbours (in case of >= 3x3x3 cube). Then each of those neighbours node will be polled by order of entrance and their neighbours will be offered at the end of the queue. The proceeder keep running until no unvisited neighbour is left.

**Code explanation:**<br>
First we need to know the size of the cube. A cube of 3x3x3 mean we should create 27 nodes. I created a method called `generateCubeGraph()` which will generate input string to inform the program about the relation between neighbour nodes. An example of return output by this method:

    27 54
    0 1
    0 3
    0 9
    1 2
    1 4
    1 10
    etc..

The first two values are respectively, the number of nodes, and the number of links/edges between neighbour nodes. The rest of the lines are the connection between nodes. For example the first line tells that node zero is connected to node 1, etc... Note that this is an undirected graph, so when the program store the link between nodes, it store from node x to node y and from node y to node x. <br>
After generating the input, `build()` method will store the links between nodes in an adjacency list. Another array is created to count how many edge have been created for every node. <br>
After storing the links, all we need to do is traverse the cube graph using BFT algorithm. Check above description on how it works and read the implementation for more understanding of how it works.<br>
The printing methods are optional, they help in the implementation and in the description of how the code is working.

This picture below shows how I numbered the nodes in a cube of 3x3x3 nodes. Moreover, I have added an example to show how a node is linked to its X, Y and Z neighbour (At the bottom of the picture).

![enter image description here][1]

**Output for a Cube of 3 x 3 x 3 nodes**

    Node execution order: 
    13 4 10 12 14 16 22 1 3 5 7 9 11 19 15 21 17 23 25 0 2 6 8 18 20 24 26 
    
    Nodes links:
    Node   0 linked to nodes:   1   3   9 
    Node   1 linked to nodes:   0   2   4  10 
    Node   2 linked to nodes:   1   5  11 
    Node   3 linked to nodes:   0   4   6  12 
    Node   4 linked to nodes:   1   3   5   7  13 
    Node   5 linked to nodes:   2   4   8  14 
    Node   6 linked to nodes:   3   7  15 
    Node   7 linked to nodes:   4   6   8  16 
    Node   8 linked to nodes:   5   7  17 
    Node   9 linked to nodes:   0  10  12  18 
    Node  10 linked to nodes:   1   9  11  13  19 
    Node  11 linked to nodes:   2  10  14  20 
    Node  12 linked to nodes:   3   9  13  15  21 
    Node  13 linked to nodes:   4  10  12  14  16  22 
    Node  14 linked to nodes:   5  11  13  17  23 
    Node  15 linked to nodes:   6  12  16  24 
    Node  16 linked to nodes:   7  13  15  17  25 
    Node  17 linked to nodes:   8  14  16  26 
    Node  18 linked to nodes:   9  19  21 
    Node  19 linked to nodes:  10  18  20  22 
    Node  20 linked to nodes:  11  19  23 
    Node  21 linked to nodes:  12  18  22  24 
    Node  22 linked to nodes:  13  19  21  23  25 
    Node  23 linked to nodes:  14  20  22  26 
    Node  24 linked to nodes:  15  21  25 
    Node  25 linked to nodes:  16  22  24  26 
    Node  26 linked to nodes:  17  23  25 
    
    Nodes on Layers: // Check the picture above to know what the below layers are.
    Layer: 0
      0   3   6 
      9  12  15 
     18  21  24 
    
    Layer: 1
      1   4   7 
     10  13  16 
     19  22  25 
    
    Layer: 2
      2   5   8 
     11  14  17 
     20  23  26 


  [1]: http://i.stack.imgur.com/WBklg.png
