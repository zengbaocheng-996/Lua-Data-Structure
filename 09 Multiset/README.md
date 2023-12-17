# MultiSet

|              |                                                |
| ------------ | ---------------------------------------------- |
| count(e)     | Returns how many e objects are in the multiset |
| removeAll(e) | Removes all e objects from the multiset        |

```lua
MSet = {}
Mset.__index = MSet

function MSet:new()
    local l = {__size = 0}
    return setmetatable(l, self)
end

function MSet:add(elem)
    self[elem] = (self[elem] or 0) + 1
    self.__size = self.__size + 1
end

function MSet:remove(elem)
    local current = self[elem] or 0
    if current > 0 then
        current = current - 1
        self.__size = self.__size - 1
    end
    self[elem] = current
end

function MSet:member(elem)
    return ((self[elem] or 0) > 0)
end

function MSet:count(elem)
    return self[elem] or 0
end

function MSet:size()
    return self.__size
end

function MSet:union(b)
    for k, v in pairs(b) do
        if k ~= '__size' then
            local bcount= v or 0
            self[k] = (self[k] or 0) + bcount
            self.__size = self.__size + bcount
        end
    end
end

function MSet:intersect(b)
    for k, acount in pairs(self) do
        if k ~= '__size' then
            local bcount = b[k] or 0
            self[k] = math.min(acount, bcount)
            self.__size = self.__size - math.abs(acount - bcount)
        end
    end
end

function MSet:difference(b)
    for k, bcount in pairs(b) do
        if k ~= '__size' then
            local acount = self[k] or 0
            local reduced = acount - bcount
            if acount >= bcount then
                self[k] = acount - bcount
                self.__size = self.__size - bcount
            else
                self[k] = nil
                self.__size = self.__size - acount
            end
        end
    end
end
```

