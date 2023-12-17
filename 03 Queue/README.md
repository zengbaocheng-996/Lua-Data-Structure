# Queue

|            |                                                              |                            |
| ---------- | ------------------------------------------------------------ | -------------------------- |
| enqueue(e) | Insert element e at the end of the queue                     | table.insert(queue, value) |
| dequeue()  | Remove and return the object at the front of the queue       | table.remove(queue, 1)     |
| front()    | Return the object at the front of the queue without removing it | queue[1]                   |

```lua
local modenv = getfenv() -- module environment

function new()
    return setmetatable({first = 1, last = 0}, {__index = modenv})
end

function insert(Q, v)
    assert(v ~= nil, "cannot insert nil")
    local last = Q.last + 1
    Q[last]    = v
    Q.last     = last
end

function retrieve(Q)
    local first = Q.first
    assert(Q.last >= first, "cannot retrieve from empty queue")
    local v     = Q[first]
    Q[first]    = nil -- allow GC
    Q.first     = first + 1
    return v
end

function isempty(Q)
    return Q.last < Q.first
end
```

