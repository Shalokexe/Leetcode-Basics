# Leetcode-Basics
Daily LeetCode solutions to build consistency, improve problem-solving, and keep my coding streak alive.


Use a single pointer and remove duplicates in place by skipping equal next nodes. Since the list is sorted, duplicates are always adjacent, so the solution is 
𝑂
(
𝑛
)
O(n) time and 
𝑂
(
1
)
O(1) extra space.

Idea
Traverse the list with curr.

While curr and curr.next exist:

If curr.val == curr.next.val, delete the next node by linking curr.next = curr.next.next.

Otherwise, move curr forward.

Python solution
python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        curr = head

        while curr and curr.next:
            if curr.val == curr.next.val:
                curr.next = curr.next.next
            else:
                curr = curr.next

        return head
Why it works
Because the list is sorted, all equal values appear next to each other. So whenever two adjacent nodes have the same value, keeping the first and bypassing the second removes the duplicate correctly.

Example
Input: [1,1,2,3,3]
Process:

1 == 1, skip the second 1

1 != 2, move forward

2 != 3, move forward

3 == 3, skip the second 3

Output: [1,2,3]

Complexity
Time: 
𝑂
(
𝑛
)
O(n)

Space: 
𝑂
(
1
)
O(1)

I can also give you a Java, C++, or debug-trace version for your GitHub LeetCode repo.



# 33. Search in Rotated Sorted Array

Problem Description
You are given an integer array nums that was originally sorted in ascending order with all distinct values. However, this array may have been left rotated at some unknown pivot index k (where 1 <= k < nums.length).

A left rotation at index k means the array is rearranged from its original order [nums[0], nums[1], ..., nums[n-1]] to [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]].

For example:

Original sorted array: [0,1,2,4,5,6,7]
After left rotation by 3 indices: [4,5,6,7,0,1,2]
Your task is to search for a given target value in this possibly rotated array and return its index. If the target is not found in the array, return -1.

Key Requirements:

The algorithm must have O(log n) runtime complexity
The array contains distinct values (no duplicates)
The array may or may not be rotated
The challenge is to efficiently search in this rotated sorted array without first finding the rotation point or restoring the original order. Since the required time complexity is O(log n), a linear search is not acceptable - you need to use a modified binary search approach that can handle the rotation.

# SOLUTION :

class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid

            # Check which half is sorted
            if nums[left] <= nums[mid]:
                # Left half is sorted
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            else:
                # Right half is sorted
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1

        return -1












# 111. Minimum Depth of Binary Tree
Easy
Topics
premium lock icon
Companies
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

 

Example 1:

<img width="432" height="302" alt="image" src="https://github.com/user-attachments/assets/c41500f4-0902-427b-b15d-aa4ef617de89" />


Input: root = [3,9,20,null,null,15,7]
Output: 2
Example 2:

Input: root = [2,null,3,null,4,null,5,null,6]
Output: 5
 

Constraints:

The number of nodes in the tree is in the range [0, 105].
-1000 <= Node.val <= 1000

# Solution;

class Node:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def binary_tree_min_depth(root: Node) -> int:
    # WRITE YOUR BRILLIANT CODE HERE
    return 0

def build_tree(nodes, f):
    val = next(nodes)
    if val == "x":
        return None
    left = build_tree(nodes, f)
    right = build_tree(nodes, f)
    return Node(f(val), left, right)

if __name__ == "__main__":
    root = build_tree(iter(input().split()), int)
    res = binary_tree_min_depth(root)
    print(res)



# 96. Unique Binary Search Trees
Medium
Topics
premium lock icon
Companies
Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.

 

Example 1:

<img width="901" height="222" alt="image" src="https://github.com/user-attachments/assets/3b7b8e64-a9fc-439b-91e9-aed69431f906" />


Input: n = 3
Output: 5
Example 2:

Input: n = 1
Output: 1
 

Constraints:

1 <= n <= 19


# Solution:

class Solution:
  def numTrees(self, n: int) -> int:
    # dp[i] := the number of unique BST's that store values 1..i
    dp = [1, 1] + [0] * (n - 1)

    for i in range(2, n + 1):
      for j in range(i):
        dp[i] += dp[j] * dp[i - j - 1]

    return dp[n]
