# Leetcode-Mental-Model
This is to help myself build a mental representation on how to approach Leetcode problem


### Binary Search in Rotated & Sorted Array
* Find pivot, so we can seperate an array into two part
```
[0,1,2,3,4] # no pivot
[4,0,1,2,3] # [4] [0,1,2,3]
[3,4,0,1,2] # [3,4] [0,1,2]
[2,3,4,0,1] # [2,3,4] [0,1]
[1,2,3,4,0] # [1,2,3,4] [0]
```
* How do we find pivot ?
This is a good exercise to start https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/. We search for the minimum in a rotated sorted array then we would see if it's on index 0.

Basic idea is:
i) we need to find the `mid`, `l + (r-l)//2`, if arr[mid] > arr[r], then violates the property that it's always increasing, so the smallest is somewhere in the right </br>
ii) When calculating `mid`, there are two scenarios, if we do `while l < r`, if we have `0 1 2`, mid will be 1, but if we have `0 1` mid will be 0. </br>
iii) We know that we reach the minimum when: </br>
-> `arr[mid] > arr[mid+1]` </br>
-> `arr[mid-1] > arr[mid]` </br>
We need to be careful for when `arr[mid-1] > arr[mid]` is because if we have `[0 1]` mid will be 0, and `arr[mid-1]` = `arr[-1]`, which will not be accepted in some case </br> 
iv) if we have a case that hasn't rotated but we have two elements `[0 1]`, it will not passed the two conditions we mentioned `arr[mid] > arr[mid+1]`/`arr[mid-1] > arr[mid]` so in that case, we know we just return the left `arr[l]`
whole code will look like
``` python
        l = 0
        r = len(nums)-1

        while l < r:
            mid = l + (r - l) // 2

            if nums[mid] > nums[mid+1]:
                return nums[mid+1]
            if mid != 0 and nums[mid-1] > nums[mid]:
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
```
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
