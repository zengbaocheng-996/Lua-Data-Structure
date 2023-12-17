# Lists

### Array List

|           |                                                      |
| --------- | ---------------------------------------------------- |
| get(i)    | Return the element of the list with index i          |
| set(i, e) | Replace with e and return the element at index i     |
| add(i, e) | Insert a new element e into the list to have index i |
| remove(i) | Remove the element at index i                        |

```lua
List = {}
List.__index = List

function List:new()
	return setmetatable({__size = 0}, self)
end

function List:get(i)
    return self[i]
end

function List:set(i, e)
	self[i] = e
end

function List:add(i, e)
	table.insert(self, i, e)
    self.__size = self.__size + 1
end

function List:remove(i)
	table.remove(self, i)
    self.__size = self.__size - 1
end

function List:size()
	return self.__size
end
```

### Node List

|                 |                                                            |
| --------------- | ---------------------------------------------------------- |
| first()         | Return the first node                                      |
| last()          | Return the last node                                       |
| next(p)         | Return the node following node p                           |
| prev(p)         | Return the node preceding node p                           |
| set(p, e)       | Replace node p's current value with e                      |
| addFirst(e)     | Insert a new first node with value e                       |
| addLast(e)      | Insert a new last node with value e                        |
| addBefore(p, e) | Insert a new node with value e into the list before node p |
| addAfter(p, e)  | Insert a new node with value e into the list after node p  |
| remove(p)       | Remove and return node p                                   |

```lua
NList = {}
NList.__index = NList

function NList:new()
	local l = {head = {}, tail = {}, __size = 0}
    l.head.__next, l.tail.__prev = l.tail, l.head
    return setmetatable(l, self)
end

function NList:first()
	if self.__size > 0 then
    	return self.head.__next
    else
       return nil 
    end
end

function NList:last()
	if self.__size > 0 then
    	return self.tail.__prev
    else
       return nil 
    end
end

function NList:set(node, elem)
    node.value = elem
end

function NList:next(node)
	if node.__next ~= self.tail then
    	return node.__next
    else
        return nil
    end
end

function NList:prev(node)
    if node.__prev ~= self.head then
        return node.__prev
    else
        return nil
    end
end

function NList:addFirst(elem)
	local node = 
        {__prev = self.head, value = elem, __next = self.head.__next}
    node.__next.__prev = node
    self.head.__next = node
 	self.__size = self.__size + 1
end

function NList:addLast(elem)
	local node =
    	{__prev = self.tail.__prev, value = elem, __next = self.tail}
	node.__prev.__next = node
    self.tail.__prev = node
    self.__size = self.__size + 1
end

function NList:addBefore(node, elem)
    local new_node =
    	{__prev = node, value = elem, __next = node.__next}
    node.__next = new_node
    new_node.__next.__prev = new_node
    self.__size = self.__size + 1
end

function NList:remove(node)
	node.__prev.__next = node.__next
    node.__next.__prev = node.__prev
    self.__size = self.__size + 1
end

function NList:size()
	return self.__size
end
```

### Skip List

```lua
function SkipList:find(k)
	local p = self.TopLeft
    while p.below do
    	p = p.below
        while k >= p.next.key do
        	p = p.next
        end
    end
end
```
