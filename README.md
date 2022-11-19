# Largest-Independent-Set-2
Largest Independent Set 2

Given a Binary Tree of size N, find the size of the Largest Independent Set(LIS) in it. A subset of all tree nodes is an independent set if there is no edge between any two nodes of the subset. Your task is to complete the function LISS(), which finds the size of the Largest Independent Set.

Here we are trying to reduce the number of function calls, we are trying to avoid the number of function calls.
The main focus of this code is to stop calculating the LIS of the same code again and again.

```cpp
class Solution {
    public int LISS(Node node){
        //Write your code here  
        if(node == null)
        return 0;
        
        //MAIN CODE
        HashMap<Node,Integer> hmp = new HashMap<Node,Integer>();
        return helper(node,hmp);
        
        
        
    }
    public int helper( Node node,HashMap<Node,Integer> hmp){
        if(node == null)
        return 0;
        if(hmp.containsKey(node)){
            return hmp.get(node);
        }
        int leftChildSum = node.left!=null?(LISS(node.left)):0;
        int rightChildSum = node.right!=null?(LISS(node.right)):0;
        
        int leftLGrandChildSum = node.left!=null&&(node.left.left!=null)?LISS(node.left.left):0;
        int leftRGrandChildSum = node.left!=null&&(node.left.right!=null)?LISS(node.left.right):0;
        int rightLGrandChildSum = node.right!=null&&(node.right.left)!=null?LISS(node.right.left):0;
        int rightRGrandChildSum = node.right!=null&&(node.right.right)!=null?LISS(node.right.right):0;
        
        int childVal = leftChildSum+rightChildSum;
        int grandChildVal = leftLGrandChildSum+leftRGrandChildSum+rightLGrandChildSum+rightRGrandChildSum;
        
        hmp.put(node,Math.max(1+grandChildVal,childVal));
        return hmp.get(node);
    }

```
Time Complexity : O(Number of nodes)
Space Complexity : O(Depth of binary tree)
