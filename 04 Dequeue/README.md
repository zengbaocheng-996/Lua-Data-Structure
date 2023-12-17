# Dequeue

|             |                                                              |
| ----------- | ------------------------------------------------------------ |
| addFirst(e) | Insert element e at the beginning of the dequeue             |
| addLast(e)  | Insert element e at the end of the dequeue                   |
| getFirst()  | Remove and return the object at the front of the dequeue     |
| getLast()   | Remove and return the object at the end of the dequeue       |
| first()     | Return the object at the front of the dequeue without removing it |
| last()      | Return the object at the end of the dequeue without removing it |

```lua
Dequeue = {}
Dequeue.__index = Dequeue

function Dequeue:new()
	return setmetatable({__first = 0, __last = -1}, self)
end

function Dequeue:addFirst(elem)
	self.__first = self.__first - 1
    self[self.__first] = elem
end

function Dequeue:addLast(elem)
	self.__last = self.__last + 1
    self[self.__last] = elem
end

function Dequeue:first()
	return self[self.__first]
end

function Dequeue:last()
	return self[self.__last]
end

function Dequeue:getFirst()
    if self.__first > self.__last then return nil end
    local result = self[self.__first]
    self.__first = self.__first + 1
    return result
end

function Dequeue:getLast()
    if self.__first > self.__last then return nil end
	local result = self[self.__last]
    self.__last = self.__last - 1
    return result
end

function Dequeue:size()
    return (self.__last - self.__first + 1)
end
```

```lua
NDequeue = {}
NDequeue.__index = NDequeue

function NDequeue:new()
    local l = {nlist = NList:new()}
    return setmetatable(l, self)
end

function NDequeue:addFirst(elem)
    self.nlist:addFirst(elem)
end

function NDequeue:addLast(elem)
    self.nlist:addLast(elem)
end

function NDequeue:getFirst()
    local result = self.nlist:first()
    if result then
        self.nlist:remove(result)
        return result.value
    else
        return nil
    end
end

function NDequeue:getLast()
    local result = self.nlist:last()
    if result then
        self.nlist:remove(result)
        return result.value
    else
        return nil
    end
end

function NDequeue:first()
    return self.nlist:first().value
end

function NDequeue:last()
    return self.nlist:last().value
end

function NDequeue:size()
    return self.nlist:size()
end
```

