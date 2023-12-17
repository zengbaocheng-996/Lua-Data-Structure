# Graph

|                   |                                                           |
| ----------------- | --------------------------------------------------------- |
| vertices()        | Return a list of the vertices of the graph                |
| edges()           | Return a list of the edges of the graph                   |
| incidentEdges(v)  | Return a list of all edges where one endpoint is vertex v |
| areAdjacent(v, u) | Test whether verticecs v and u are adjacent               |
| insertEdge(v, u)  | Make vertices u and v adjacent                            |
| removeEdge(v, u)  | Make vertices u and v non-adjacent                        |

```lua
Graph = {}
Graph.__index = Graph

function Graph:new(n)
    local l = {__size = n}
    local vertices = {}
    for i = 1, n do
        table.insert(vertices, i)
    end
    l.__vertices = vertices
    local graph = {}
    for i = 1, n do
        table.insert(graph, {})
    end
    l.__graph = graph
    return setmetatable(l, self)
end

function Graph:vertices()
    return self.__vertices
end

function Graph:incidentEdges(v)
    local result = {}
    for i = 1, v-1 do
        if self.__graph[i][v] then table.insert(result, i) end
    end
    for i, _ in pairs(self.__graph[v]) do
        table.insert(result, i)
    end
    return result
end

function Graph:areAdjacent(v, u)
    return ((self.__graph[v][u] or self.__graph[u][v]) or false)
end

function Graph:insertEdge(v, u)
    if u < v then v, u = u, v end
    self.__graph[v][u] = true
end

function Graph:removeEdge(v, u)
    if u < v then v, u = u, v end
    self.__graph[v][u] = nil
end
```

