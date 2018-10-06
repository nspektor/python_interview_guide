
# Mark Abramov's super awesome Google interview guide
## Made by your 1 tru 😍

# Table of Contents
1. Data Structures
    - Lists
    - Dictionaries
    - Sets
    - Binary Trees
2. Graphs
3. BFS
4. DFS
5. Objects

    

## Data Structures
### Lists


```python
greeting = list('HiMark') #string to list
greeting
```


```python
greeting.append('!') #adds 1 element to the end
```


```python
greeting.extend(['<', '3']) #extend appends all the elements of the given list
```


```python
greeting
```


```python
greet_string = ''.join(greeting) #joins with '' between every element
```


```python
greeting * 2 # the list twice
```


```python
greet_string * 2 #the string twice
```

Converting to Ascii:
    - ord(c) converts a character to its ascii value
    - doing this in a list comprehenstion (thats what the [ for in ] thing is called) does it for every char in the string


```python
greet_ascii = [ord(c) for c in greet_string]
greet_ascii
```


```python
''.join(chr(i) for i in greet_ascii) # you can do a little list comprehension inside a method call without the []
```


```python
sorted_ascii = sorted(greet_ascii)
sorted_ascii
```

- you can use the optional key argument and pass it a lambda function
- `lambda VARIABLE_NAME_YOU_DEFINE: whatever you want to do to the VAR`


```python
greeting.sort(key = lambda char: char.upper()) 
greeting = greeting[::-1] # REVERSE the list
greeting
```

#### List Complexities

| Operation | Big O      |
|-----------|------------|
| append    | O(1)       |
| Pop Last  | O(1)       |
| Insert    | O(n)       |
| Get/Set   | O(1)       |
| Length    | O(1)       |
| Sort      | O(n log n) |


---
### Dictionaries
- `len(d)` returns the number of key,value pairs
- `del d[k]` deletes the key k and its value
- `d.pop(k)` deletes key and value and returns the value
    - can put a default value for if k isnt in the dict: `d.pop(k, 'nope')`
    - otherwise there will be a *KeyError*
- `if k in d` if there is a key k in dictionary d
- `d1.update(d2)` merges the dictionaries
- `L = list(D)` converts dictionary into list of 2-item tuples
- `D = dict(zip(L1, L2))` zips and converts 2 lists into a dictionary


```python
rappers = {} # creating empty dictionary
```


```python
rappers['Kanye'] = 1
rappers['J Cole'] = 2
rappers['Nicki Minaj'] = 15
rappers
```


```python
len(rappers)
```


```python
for ranking in rappers.values(): #also: rappers.keys()
    print(ranking)
```


```python
for rapper, ranking in rappers.items():
    print('the number ', ranking, ' rapper is ', rapper)
```

#### Dictionary Complexities
| Operation | Big O      |
|-----------|------------|
| Delete    | O(1)       |
| Insert    | O(n)       |
| Get/Set   | O(1)       |
| Length    | O(1)       |
| Sort      | O(n log n) |

---
### Sets
- like a 1 dimensional dictionary
- unordered, no duplicates


```python
your_friends = set()
your_friends.add("Maxwell")
your_friends.add("Stelios")
your_friends.add("Jazmyn")
your_friends
```


```python
your_friends.add("Maxwell")
your_friends
```

    - oh well, guess you cant have 2 Maxwells

#### Set Complexities
| Operation | Big O      |
|-----------|------------|
| Delete    | O(1)       |
| x in s    | O(1)       |
| Get/Set   | O(1)       |
| Length    | O(1)       |


### Binary Trees 
- not native to python but heres a nice implementation (and a little intro to how classes work)


```python
class Node:

    def __init__(self, data):
        # init is the constructor
        self.left = None
        self.right = None
        self.data = data

    def insert(self, data): # every method takes self
        # Compare the new value with the parent node
        if self.data:
            if data < self.data:
                if self.left is None:
                    self.left = Node(data)
                else:
                    self.left.insert(data)
            elif data > self.data:
                if self.right is None:
                    self.right = Node(data)
                else:
                    self.right.insert(data)
        else:
            self.data = data

# Print the tree - not a great representation but ya know
    def PrintTree(self):
        if self.left:
            self.left.PrintTree()
        print(self.data),
        if self.right:
            self.right.PrintTree()

# Use the insert method to add nodes
root = Node(12)
root.insert(6)
root.insert(14)
root.insert(3)

root.PrintTree()# notice you dont have to write self

```

#### Binary Tree Complexities
| Operation | Big O      |
|-----------|------------|
| Search    | O(n)       |
| Insertion | O(n)       |
| Deletion  | O(n)       |

#### Binary Search Tree Complexities
| Operation | Big O      |
|-----------|------------|
| Search    | O(h)-height|
| Insertion | O(h)       |
| Deletion  | O(h)       |

#### AVL Tree Complexities
| Operation | Big O      |
|-----------|------------|
| Search    | O(log n)   |
| Insertion | O(log n)   |
| Deletion  | O(log n)   |


### Graphs
- can be represented in Python as a dictionary
![graph](http://faculty.cs.niu.edu/~freedman/340/340notes/gifImages/340graph7.gif)



```python
graph = {
    'v1': ['v2', 'v4', 'v3'],
    'v2': ['v4', 'v5'],
    'v3': ['v6'],
    'v4': ['v3', 'v6', 'v7'],
    'v5': ['v4', 'v7'],
    'v6': [],
    'v7': ['v6']
}
```


```python
graph
```

- Find Path


```python
 def find_path(graph, start, end, path=[]):
        path = path + [start]
        if start == end:
            return path
        if not start in graph.keys():
            return None
        for node in graph[start]:
            if node not in path:
                newpath = find_path(graph, node, end, path)
                if newpath: return newpath
        return None
```


```python
find_path(graph, 'v1', 'v6') #clearly not the best path, just A path
```

I didnt really have time to do this in my own words but here is some stuff I took from [Geeks for Geeks](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)


```python

# Python3 Program to print BFS traversal 
# from a given source vertex. BFS(int s) 
# traverses vertices reachable from s. 
from collections import defaultdict 
  
# This class represents a directed graph 
# using adjacency list representation 
class Graph: 
  
    # Constructor 
    def __init__(self): 
  
        # default dictionary to store graph 
        self.graph = defaultdict(list) 
  
    # function to add an edge to graph 
    def addEdge(self,u,v): 
        self.graph[u].append(v) 
  
    # Function to print a BFS of graph 
    def BFS(self, s): 
  
        # Mark all the vertices as not visited 
        visited = [False] * (len(self.graph)) 
  
        # Create a queue for BFS 
        queue = [] 
  
        # Mark the source node as  
        # visited and enqueue it 
        queue.append(s) 
        visited[s] = True
  
        while queue: 
  
            # Dequeue a vertex from  
            # queue and print it 
            s = queue.pop(0) 
            print (s, end = " ") 
  
            # Get all adjacent vertices of the 
            # dequeued vertex s. If a adjacent 
            # has not been visited, then mark it 
            # visited and enqueue it 
            for i in self.graph[s]: 
                if visited[i] == False: 
                    queue.append(i) 
                    visited[i] = True
  
# Driver code 
  
# Create a graph given in 
# the above diagram 
g = Graph() 
g.addEdge(0, 1) 
g.addEdge(0, 2) 
g.addEdge(1, 2) 
g.addEdge(2, 0) 
g.addEdge(2, 3) 
g.addEdge(3, 3) 
  
print ("Following is Breadth First Traversal"
                  " (starting from vertex 2)") 
g.BFS(2) 
  
# This code is contributed by Neel
```

aaaand for [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 


```python

# Python program to print DFS traversal from a 
# given given graph 
from collections import defaultdict 
  
# This class represents a directed graph using 
# adjacency list representation 
class Graph: 
  
    # Constructor 
    def __init__(self): 
  
        # default dictionary to store graph 
        self.graph = defaultdict(list) 
  
    # function to add an edge to graph 
    def addEdge(self,u,v): 
        self.graph[u].append(v) 
  
    # A function used by DFS 
    def DFSUtil(self,v,visited): 
  
        # Mark the current node as visited and print it 
        visited[v]= True
        print(v) 
  
        # Recur for all the vertices adjacent to this vertex 
        for i in self.graph[v]: 
            if visited[i] == False: 
                self.DFSUtil(i, visited) 
  
  
    # The function to do DFS traversal. It uses 
    # recursive DFSUtil() 
    def DFS(self,v): 
  
        # Mark all the vertices as not visited 
        visited = [False]*(len(self.graph)) 
  
        # Call the recursive helper function to print 
        # DFS traversal 
        self.DFSUtil(v,visited) 
  
  
# Driver code 
# Create a graph given in the above diagram 
g = Graph() 
g.addEdge(0, 1) 
g.addEdge(0, 2) 
g.addEdge(1, 2) 
g.addEdge(2, 0) 
g.addEdge(2, 3) 
g.addEdge(3, 3) 
  
print("Following is DFS from (starting from vertex 2)")
g.DFS(2) 
  
# This code is contributed by Neelam Yadav 
```
