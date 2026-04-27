<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name:DIVYADARSHINI M      </h3>
<h3>Register Number:212224060072           </h3>
<H3>Aim:</H3>
<p>To Implement A * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>
A* Search Algorithm
<br>
1.  Initialize the open list
<br>
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)
<br>
3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"
<br>
    b) pop q off the open list
<br>
    c) generate q's 8 successors and set their 
       parents to q
<br>
    d) for each successor
    <br>
        i) if successor is the goal, stop search
        <br>
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          successor.f = successor.g + successor.
          <br>
        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor
           <br>
        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
            <br>
     end (for loop)
    <br>
    e) push q on the closed list
    <br>
    end (while loop)

## PROGRAM
```
import heapq

def astar(graph, h, start, goal):
    open_list = [(h[start], 0, start, None)]  # (f, g, node, parent)
    closed = {}
    parent = {}
    while open_list:
        f, g, node, par = heapq.heappop(open_list)
        if node in closed and closed[node] <= g:
            continue

        parent[node] = par
        closed[node] = g

        if node == goal:
            path = []
            while node:
                path.append(node)
                node = parent[node]
            return path[::-1]

        for nei, cost in graph.get(node, []):
            new_g = g + cost
            new_f = new_g + h[nei]
            heapq.heappush(open_list, (new_f, new_g, nei, node))

n, e = map(int, input().split())
graph = {}
for _ in range(e):
    u, v, w = input().split()
    w = int(w)
    graph.setdefault(u, []).append((v, w))
    graph.setdefault(v, []).append((u, w))

h = {}
for _ in range(n):
    node, val = input().split()
    h[node] = int(val)
    
start, goal = input().split()
path = astar(graph, h, start, goal)
print("Path found:", path)
```

<hr>
<h2>Sample Graph I</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

<hr>
<h2>Sample Input</h2>
<hr>
10 14 <br>
A B 6 <br>
A F 3 <br>
B D 2 <br>
B C 3 <br>
C D 1 <br>
C E 5 <br>
D E 8 <br>
E I 5 <br>
E J 5 <br>
F G 1 <br>
G I 3 <br>
I J 3 <br>
F H 7 <br>
I H 2 <br>
A 10 <br>
B 8 <br>
C 5 <br>
D 7 <br>
E 3 <br>
F 6 <br>
G 5 <br>
H 3 <br>
I 1 <br>
J 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
Path found: ['A', 'F', 'G', 'I', 'J']


<hr>
<h2>Sample Graph II</h2>


![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)


<h2>Sample Input</h2>

6 6 <br>
A B 2 <br>
B C 1 <br>
A E 3 <br>
B G 9 <br>
E D 6 <br>
D G 1 <br>
A 11 <br>
B 6 <br>
C 99 <br>
E 7 <br>
D 1 <br>
G 0 <br>

<h2>Sample Output</h2>

Path found: ['A', 'E', 'D', 'G']

### OUTPUT
<img width="388" height="472" alt="image" src="https://github.com/user-attachments/assets/ef0d1045-fea8-4cb5-b630-b42538f42f99" />
<hr>
