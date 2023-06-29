# Leetcode-Mental-Model
This is to help myself build a mental representation on how to approach Leetcode problem

### How to detect a duplication/loop
You need to remember if you have been there, a set is a good Data Structure to remember it

### Binary Search in Rotated & Sorted Array
* Find pivot, so we can seperate an array into two part
```
[0,1,2,3,4] # no pivot
[4,0,1,2,3] # [4] [0,1,2,3]
[3,4,0,1,2] # [3,4] [0,1,2]
[2,3,4,0,1] # [2,3,4] [0,1]
[1,2,3,4,0] # [1,2,3,4] [0]
```
* How do we find pivot ? <br>
This is a good exercise to start https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/. We search for the minimum in a rotated sorted array then we would see if it's on index 0. </br></br>
Basic idea is: <br>
i) we need to find the `mid`, `l + (r-l)//2`, if arr[mid] > arr[r], then violates the property that it's always increasing, so the smallest is somewhere in the right </br>
ii) When calculating `mid`, there are two scenarios, if we do `while l < r`, if we have `0 1 2`, mid will be 1, but if we have `0 1` mid will be 0. </br>
iii) We know that we reach the minimum when: </br>
-> `arr[mid] > arr[mid+1]` </br>
-> `arr[mid-1] > arr[mid]` </br>
iv) if we have a case that hasn't rotated but we have two elements `[0 1]`, it will not passed the two conditions we mentioned `arr[mid] > arr[mid+1]`/`arr[mid-1] > arr[mid]` so in that case, we know we just return the left `arr[l]`
whole code will look like
``` python
        l = 0
        r = len(nums)-1

        while l < r:
            mid = l + (r - l) // 2

            if nums[mid] > nums[mid+1]:
                return nums[mid+1]
            if nums[mid-1] > nums[mid]:
                return nums[mid] 
            
            # Detect anomoly
            if nums[mid] > nums[r]:
                l = mid + 1
            else:
                r = mid - 1

        return nums[l]
```

### Reorder List
* When we see a LinkedList, what can we do with it? </br>
-> Transverse (only going forward, no going backward) </br>
-> We can reoorder it by (add, remove) </br>
**The last thing which is pretty uncommon:** </br>
-> We can use two pointers to find the gap. Gap can be from the **end to the mid point** or any arbitary gap. </br>
-> We can use two pointers to find whether the linkedlist has a loop
* If we want to access the previous node, for example in a HashLinkedList where we get the node we want to remove but we also need to use the previous node, we should use a double linked list

### Tree
There is different ways of transversing a tree, for the first 3 , it's just the different of where you want to put the print position </br>
#### These are what we call a DFS (not inclusing detecting loop)
i) Preorder Transversal
```python
def transversal(root):
   if root == None:
     return 
   
   print(root.val)
   transversal(root.left)
   transversal(root.right)
```
ii) Inorder Transversal
```python
def transversal(root):
   if root == None:
     return 
     
   transversal(root.left)
   print(root.val)
   transversal(root.right)
```
iii) Postorder Transversal
```python
def transversal(root):
   if root == None:
     return 
     
   transversal(root.left)
   transversal(root.right)
   print(root.val)
```
#### These are what we call a BFS (not inclusing detecting loop)
iv) Level order transversal
```python
def transversal(root):
    queue = []
    queue.push(root)
    
    while(len(queue) != 0):
        head = queue.pop()
        
        if head.left != None:
           queue.push(head.left)
        if head.right != None:
           queue.push(head.right)
           
        print(head)
```
#### Tree can be produced from an array
https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/

### Trie 
![image](https://github.com/lauchokyip/Leetcode-Mental-Model/assets/42656921/4f3d2e25-2756-45ab-8a9b-aa802aa29d08)
* Instead of each TrieNode storing val, each node is storing a mapping for character to another TrieNode. We aren't using a `dict` for the mapping because mapping is slower than array in the sense that when the map is expanding or when querying, map collision will happen
* Now we have the tree, how do we know if the word ends in the characters, maybe we have trynna, and t/ r/ try etc etc will be valid if we don't know where to stop. That's why we need another attribute to know when to stop.

### Backtracking
> DFS is a general graph traversal (and search) algorithm. So it can be applied to any graph (or even forest). Tree is a special kind of Graph, so DFS works for tree as well. Backtracking is a special kind of DFS used mainly for space (memory) saving. It can be used for space saving because usually it has constraints that we need to follow so we don't transverse down the whole tree

Backtracking will often need pruning after visiting the node, so 
```python
def transversal(root):
   if root == None:
     return 
   
   doSomething()
   transversal(root.left)
   transversal(root.right)
   restoreIt()
```

**So treat backtracking the same as DFS!**

### Intervals
* A lot of times we would want to **sort the start time** first
* A lot of times we would also need to think about **making all the intervals into a straight line** (merging)
* Edge cases would be when we have [[1,2],[2,3]], this would be considered as overlapping
* How do we detect overlapping? </br> , we know the first valus is sorted, so there is only one case
  ```
  |_______|
         |_____|
  ```

