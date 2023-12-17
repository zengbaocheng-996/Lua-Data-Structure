# Partition

|             |                                                 |
| ----------- | ----------------------------------------------- |
| make_set(x) | create a singleton set containing the element x |
| merge(A, B) | Merge the sets A and B, destroying the old B    |
| find(x)     | find the set containing x                       |
| get_set(x)  | return the elements in the same set as x        |

```lua
Partition = {}
Partition.__index = Partition

function Partition:new()
    local l = {__size = 0}
    return setmetatable(l, self)
end

function Partition:make_set(x)
    self[x] = self.__size
    self.__size = self.__size + 1
end

function Partition:merge(a, b)
    local a_idx = self:find(a)
    local b_idx = self:find(b)
    for k, v in pairs(self) do
        if k ~= '__size' and v == b_idx then
            self[k] = a_idx
        end
    end
    self.__size = self.__size - 1
end

function Partition:find(x)
    return self[x]
end

function Partition:get_set(x)
    local idx = self:find(x)
    local res = {}
    for k, v in pairs(self) do
        if k ~= '__size' and v == idx then
            table.insert(res, k)
        end
    end
    return res
end
```

