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
