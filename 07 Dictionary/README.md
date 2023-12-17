# Dictionary

|              |                                        |
| ------------ | -------------------------------------- |
| find(k)      | Return a value with key k              |
| findAll(k)   | Return a list of all values with key k |
| insert(k, v) | Insert value v with key k              |
| remove(k, v) | Remove value v with key k              |
| keys()       | Return a list of keys                  |

```lua
Dictionary = {}
Dictionary.__index = Dictionary

function Dictionary:new()
    local l = {__size = 0}
    return setmetatable(l, self)
end

function Dictionary:find(k)
    local matches = self[k]
    if (matches == nil) then
        return nil
    else
        local _, match = next(matches)
        return match
    end
end

function Dictionary:findAll(k)
    return self[k]
end

function Dictionary:insert(k, v)
    local tab = self[k] or {}
    table.insert(tab, v)
    self[k] = tab
    self.__size == self.__size + 1
end

function Dictionary:remove(k, v)
    local tab = self[k]
    if tab ~= nil then
        for k, val in pairs(tab) do
            if val == v then
                tab[k] = nil
        		self.__size = self.__size - 1
            end
        end
        if next(tab) == nil then
            self[k] = nil
        end
    end
end

function Dictionary:keys()
    local keys = {}
    for k, _ in pairs(self) do
        if k ~= '__size' then
            table.insert(keys, k)
        end
    end
    return keys
end

function Dictionary:size()
    return self.__size
end
```

