<extoc></extoc>

# Binary Search - 二分搜索

__Two kinds of problems__

- Search problems in **Binary Search Tree** or **Sorted Array**
    - Using **Binary Search**
    - 广义的适用问题范围：每次循环会减少解空间，不能死循环；不能在循环中，把正确答案排除掉。
- Binary Search Tree operation problems

__Idea__

- 使用**循环**`loop`不断地移动指针`curr`。
- 使用**分类讨论**`if-else`控制指针`curr`的移动。

__Time Complexity__

- `search` - worst case $O(n)$, average $O(logn)$
- `insert` - worst case $O(n)$, average $O(logn)$
- `remove` - worst case $O(n)$, average $O(logn)$

    Worst case happen if the binary tree is structured like a linked list.

    In **Balanced Binary Search Tree**, `search`, `insert` and `remove` operations are guaranteed to be $O(logn)$. For example, **AVL Tree**, **Red-Black Tree** are balanced BST.

## Binary Search Problems

__Binary Search Code Template__

Reference: [jiuzhang](http://www.jiuzhang.com/solutions/binary-search/)

```java
/**
* @param nums: The integer array.
* @param target: Target to find.
* @return: The first position of target. Position starts from 0.
*/
public int binarySearch(int[] nums, int target) {
    # First consider the case that the input is null or empty array.
    if (nums == null || nums.length == 0) {
        return -1;
    }
    # initial condition. The end is included in the range of the num,
    # because the end is initialized to the length of nums minus one
    int start = 0, end = nums.length - 1;
    # Here, the condition should be start + 1 < end.
    # because when start == 0 and end == 1, then mid = 0
    # and the start may not be updated.
    while (start + 1 < end) { # Note: use start+1<end as the condition to continue
        int mid = start + (end - start) / 2;
        if (nums[mid] == target) {
            end = mid;
        } else if (nums[mid] < target) {
            start = mid;
            // or start = mid + 1
        } else {
            end = mid;
            // or end = mid - 1
        }
    }
    # When the loop is end, decide where the first postion of target is.
    if (nums[start] == target) {
        return start;
    }
    if (nums[end] == target) {
        return end;
    }
    return -1;
}
```

__Coding Tricks__

- __循环进入条件__
    - `start + 1 < end` - 取决于最后一次循环是否需要检查左右两个pivot确定答案
    - `start < end`
    - `start <= end`
- __调试方法__
    - 使用如下的会触发边界条件的例子测试, Eg. `[0]`, `[0, 1]`, `[0, 1, 2]`
- __二分计算__
    - `mid = start + (end - start) / 2`

### Basic Problems

- __P1. Binary Search in Sorted Array__

- __P2. Binary Search in 2D sorted matrix__

- __P3. Find the closest number to target__
    - 循环条件：`left < right - 1`
- __P4. Find the first occurance of target__

- __P5. Find the last occurance of target__

- __P6. Find the K closest number to target__
    - Find largest smaller or equal number.

- __P7. Find the smallest element that is larger than target__


### Composed Search Problems

- __P8. Find mountain peak in array__

    `1 3 7 23 57 ... 100 99 86 44 32 21`

- __P9. Binary Search in a sorted array with unknown size__

    - Step 1 - jump out
    - Step 2 - jump in
    
    | | step = 2 | step = 10 |
    |----|----|----|
    | Worst case | $n=2^{k-1}+1$ | $n=10^{k-1}+1$ |
    | Jump out - Time | $log_{2}n$ | $log_{10}n$ |
    | Jump in - Time | $log_{2}10n$ | $log_{2}2n$ |


## BST Insert & Delete Problems

- __P1. Insert in BST__
    - *Problem* : return the new root after the change.

- __P2. Delete in BST__
    - *Problem* : return the new root of the BST.
    - **Step 1**: find the node to be deleted
    - **Step 2**: delete the nodes
        - **case 1** - the node has no children.
        - **case 2** - the node has no left child.
        - **case 3** - the node has no right child.
        - **case 4** - the node has both left and right children.