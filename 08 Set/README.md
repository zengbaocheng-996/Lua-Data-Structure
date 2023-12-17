# Set

|                  |                                                      |
| ---------------- | ---------------------------------------------------- |
| add(d)           | Insert object e into the set                         |
| remove(e)        | Removes object e from the set                        |
| member(e)        | Returns a Boolean indicating whether e is in the set |
| union(A, B)      | Replace the set A with the union of A and B          |
| intersect(A, B)  | Replaces the set A with the intersection of A and B  |
| difference(A, B) | Replaces the set A with the difference of A and B    |

```lua
Set = {}
Set.__index = Set

function Set:new()
    return setmetatable({__size = 0}, self)
end

function Set:add(elem)
    local result = self[elem]
    self[elem] = true
    if not result then
        self.__size = self.__size + 1
    end
end

function Set:remove(elem)
    local result = self[elem]
    self[elem] = nil
    if result then
        self.__size = self.__size - 1
    end
end

function set:member(elem)
    return (self[elem] or false)
end

function Set:size()
	return self.__size
end

function Set:union(b)
    for k, _ in pairs(b) do
        if k ~= '__size' then
            if not self[k] then
                self.__size = self.__size + 1
            end
            self[k] = true
        end
    end
end

function Set:intersect(b)
    for k, _ in pairs(self) do
        if k ~= '__size' then
            if not b[k] then
                self.__size = self.__size - 1
                self[k] = nil
            end
        end
    end
end
```

