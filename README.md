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







# 79. Word Search
Medium
Topics
premium lock icon
Companies
Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

 

Example 1:

<img width="322" height="242" alt="image" src="https://github.com/user-attachments/assets/5f75673f-c1c2-498a-8992-c9119f1d10e5" />


Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
Example 2:

<img width="322" height="242" alt="image" src="https://github.com/user-attachments/assets/43e633e4-a1c0-46bf-a191-b99457a11b75" />



Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
Example 3:

<img width="322" height="242" alt="image" src="https://github.com/user-attachments/assets/63c86f6a-2c37-4dc6-8136-35db63e56c32" />



Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
 

Constraints:

m == board.length
n = board[i].length
1 <= m, n <= 6
1 <= word.length <= 15
board and word consists of only lowercase and uppercase English letters.




Solution:

class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        """
        Determines if a word exists in the board by traversing adjacent cells.
      
        Args:
            board: 2D grid of characters
            word: Target word to search for
          
        Returns:
            True if word exists in board, False otherwise
        """
      
        def backtrack(row: int, col: int, word_index: int) -> bool:
            """
            Performs DFS with backtracking to search for the word.
          
            Args:
                row: Current row position in board
                col: Current column position in board
                word_index: Current index in the word being matched
              
            Returns:
                True if word can be formed from current position
            """
            # Base case: reached the last character of the word
            if word_index == len(word) - 1:
                return board[row][col] == word[word_index]
          
            # Current cell doesn't match the expected character
            if board[row][col] != word[word_index]:
                return False
          
            # Mark current cell as visited by temporarily changing its value
            original_char = board[row][col]
            board[row][col] = "#"  # Use "#" as visited marker
          
            # Explore all four directions: up, right, down, left
            directions = [(-1, 0), (0, 1), (1, 0), (0, -1)]
          
            for delta_row, delta_col in directions:
                next_row = row + delta_row
                next_col = col + delta_col
              
                # Check if next position is valid and not visited
                if (0 <= next_row < rows and 
                    0 <= next_col < cols and 
                    board[next_row][next_col] != "#"):
                  
                    # Recursively search from the next position
                    if backtrack(next_row, next_col, word_index + 1):
                        board[row][col] = original_char  # Restore before returning
                        return True
          
            # Backtrack: restore the original character
            board[row][col] = original_char
            return False
      
        # Get board dimensions
        rows = len(board)
        cols = len(board[0])
      
        # Try starting the search from every cell in the board
        for start_row in range(rows):
            for start_col in range(cols):
                if backtrack(start_row, start_col, 0):
                    return True
      
        return False

 
