<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name:       </h3>
<h3>Register Number:           </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>



1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
   ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
successor.f = successor.g + successor.h
          
iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
            end (for loop)
  
e) push q on the closed list
end (while loop)


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
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)


<hr>
<h2>Sample Input</h2>
<hr>
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
<hr>
<h2>Sample Output</h2>
<hr>
Path found: ['A', 'E', 'D', 'G']

<H3>Program:</H3>

```

H_dist = {}

def aStarAlgo(start, goal):
    open_set = {start}
    closed_set = set()
    g = {start: 0}
    parent = {start: start}

    while open_set:
        n = min(open_set, key=lambda v: g[v] + H_dist[v])

        if n == goal:
            path = []
            while parent[n] != n:
                path.append(n)
                n = parent[n]
            path.append(start)
            path.reverse()
            print("Path found:", path)
            return

        open_set.remove(n)
        closed_set.add(n)

        for m, cost in Graph_nodes.get(n, []):
            new_g = g[n] + cost

            if m not in g or new_g < g[m]:
                g[m] = new_g
                parent[m] = n
                open_set.add(m)
                closed_set.discard(m)

    print("Path does not exist!")


Graph_nodes = {}
n, e = map(int, input().split())

for i in range(e):
    u, v, cost = input().split()
    cost = int(cost)
    Graph_nodes.setdefault(u, []).append((v, cost))
    Graph_nodes.setdefault(v, []).append((u, cost))

for i in range(n):
    node, h = input().split()
    H_dist[node] = int(h)

start = input()
goal = input()

aStarAlgo(start, goal)

```
<H3>output:</H3>

<img width="552" height="830" alt="image" src="https://github.com/user-attachments/assets/ed14086d-4a86-48c8-9d56-83a4a19230ec" />
