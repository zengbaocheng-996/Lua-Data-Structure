# Trees

|                      |                                                              |
| -------------------- | ------------------------------------------------------------ |
| root()               | Return the tree's root                                       |
| addRoot(e)           | Create a root node with value e                              |
| parent(v)            | Return the parent of v                                       |
| children(v)          | Return a list containing the children of node v              |
| insertChild(v, i, e) | Create a new node with value e and insert it as the i-th child of node v |
| isInternal(v)        | Test whether node v is internal                              |
| isExternal(v)        | Test whether node v is external                              |
| isRoot(v)            | Test whether node v is the root                              |
| replace(v, e)        | Replace with e and return the element stored at v            |
| remove(v)            | Remove the subtree rooted at node v                          |
| left(v)              | Return the left child of node v                              |
| right(v)             | Return the right child of node v                             |
| insertLeft(v, e)     | Create a new node with value e and insert it as node v's left child |
| insertRight(v, e)    | Create a new node with value e and insert it as node v's right child |

### Linked-node trees

```lua
NTree = {}
NTree.__index = Ntree

function NTree:new()
    return setmetatable({__size = 0}, self)
end

function NTree:root()
    return self.__root
end

function NTree:addRoot(elem)
    self.__root = {value = elem}
    self.__size = 1
    return self.__root
end

function NTree:parent(node)
    return node.__parent
end

function NTree:left(node)
    return node.__left
end

function NTree:right(node)
    return node.__right
end

function NTree:insertLeft(node, elem)
    local new_node = {value = elem, __paren = node}
    node.left = new_node
    self.__size = self.__size + 1
    return new_node
end

function NTree:insertRight(node, elem)
    local new_node = {value = elem, __parent = node}
    node.__right = new_node
    self.__size = self.__size + 1
    return new_node
end

function NTree:isInternal(node)
    return node.__left or node.__right
end

function NTree:isExternal(node)
    return not self:isInternal(node)
end

function NTree:isRoot(node)
    return (node == self.__root)
end

function Ntree:replace(node, elem)
	node.value = elem
end

function NTree:remove(node)
    local parent = node.__parent
    local i_am_left_child = (parent.__left == node)
    if i_am_left_child then
        parent.__left = nil
    else
        parent.__right = nil
    end
    self.__size = self.__size - 1
end

function NTree:size()
	return self.__size
end
```

### Array-based trees

```lua
ATree = {}
ATree.__index = ATree

function ATree:new()
    return setmetatable({__size = 0}, self)
end

function ATree:root()
    return self[1]
end

function ATree:addRoot()
    self[1] = elem
    self.__size = 1
end

function ATree:parent(node)
    return math.floor(node/2)
end

function ATree:left(node)
    return 2 * node
end

function ATree:right(node)
    return 2 * node + 1
end

function ATree:insertLeft(node, elem)
    self[2 * node] = elem
    self.__size = self.__size + 1
end

function ATree:insertRight(node, elem)
    self[2 * node + 1] = elem
    self.__size = self.__size + 1
end

function ATree:isInternal(node)
    return (self[2 * node] ~= nil or self[2 * node + 1] ~= nil)
end

function ATree:isExternal(node)
    return not self:isInternal(node)
end

function ATree:isRoot(node)
    return (node == 1)
end

function ATree:replace(node, elem)
    self[node] = elem
end

function ATree:subsize(node)
    if self[node] == nil then
        return 0
    else
        return 1 + self:subsize(self:left(node)) + self:subsize(self:right(node))
    end
end

function ATree:remove(node)
    local count = self:subsize(node)
    self[node] = nil
    self.__size = self.__size - count
end

function ATree:size()
    return self.__size
end
```

