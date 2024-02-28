# 314. Binary Tree Vertical Order Traversal

# Thought

1. 输出需要设置好每一个col的List
2. 每个List是【1，2 等的节点值
3. 可以由一个list【node1，node2产生上述list
4. 然而缺失了col的地址信息，所以需要一个map<col, ArrayList>
5. 走常规的bfs，root进queue，左右孩子加queue
6. 具体的是queue<Pair<col,node>>
7. queue和map什么关系呢？每到一个新的节点先把queue里的拿出来放map

# Pseudocode

Function verticalOrder(root: TreeNode) -> List of List of Integers

```
If root is null
		Return empty list

Initialize ans as an empty list of lists
Initialize colMap as a new HashMap mapping integers to array lists
Initialize que as a new LinkedList of Pairs of Integer and TreeNode
Initialize minColumn and maxColumn as 0

Offer a new pair of 0 and root to the queue

While the queue is not empty
    Dequeue a pair (col, node) from the queue

    If colMap does not contain col
        Put col in colMap with a new ArrayList

    Add node's value to the ArrayList at col in colMap

    If node has a left child
        Offer a new pair of col-1 and node's left child to the queue
        Update minColumn to be the minimum of minColumn and col-1

    If node has a right child
        Offer a new pair of col+1 and node's right child to the queue
        Update maxColumn to be the maximum of maxColumn and col+1

For each column index from minColumn to maxColumn inclusive
    Add the ArrayList from colMap corresponding to the current column to ans

Return ans

```

Class Pair

```
Private key of generic type K
Private value of generic type V

Constructor Pair(key: K, value: V)
    this.key = key
    this.value = value

Function getKey() -> K
    Return key

Function getValue() -> V
    Return value

```

# Details

1. Map<Integer, ArrayList> columnTable = new HashMap();
    1. !hashmap.containsKey(a)
    2. hashmap.put(a, new ArrayList<Integer>()), hashmap.get(a).add(b)
    3. List<Integer> sortedKeys = new ArrayList<>(columnTable.keySet());
    -> Collections.sort(sortedKeys);
2. Queue<Pair<TreeNode, Integer>> queue = new LinkedList<>();
3. Pair.getKey()
4. Pair.getValue()
5. class Pair<K, V>