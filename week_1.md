# Grind 75
## Week 1
### Two Sum
```golang
func twoSum(nums []int, target int) []int {
    numMap := make(map[int]int)
    for i, num := range nums {
        if pos, contains := numMap[target-num]; contains {
            return []int{pos, i}
        }
        numMap[num] = i
    }
    return []int{}
```

### Valid Parentheses
``` typescript
function isValid(s: string): boolean {
    let mappings = {
        ']':'[',
        ')':'(',
        '}':'{',
    }
    let stack = []
     for(let c of s) {
        // if closing brace
        if(mappings[c]) {
           // find top element of stack.
           // for inital run, it may be null or undefined.
            let topElement = stack.pop();
        
            // if top of stack not equal to a corresponding opening brace return false
            if (topElement !== mappings[c]) return false;
        } else {
            // otherwise assume that it's an opening brace.
            stack.push(c)
        }
    }
    return stack.length === 0;
};
```
### Merge Two Sorted Lists
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function mergeTwoLists(l1: ListNode | null, l2: ListNode | null): ListNode | null {
    // initialize a basic node
    let prehead = new ListNode(-1);
    // current node points to initial node.
    let prev = prehead;
    // keep looping until end of either list is reached.
    while(l1 !== null && l2 !== null) {
        // if beginning of first list lesser equal to secon
        if (l1.val <= l2.val) {
            // then point pointer's next location to first list first node
            prev.next = l1;
            // move first list start to second element
            l1 = l1.next;
        } else {
            // else point pointer's next location to second list first node
            prev.next = l2;
            // then move second list start to second element
            l2 = l2.next;
        }
        // move pointer
        prev = prev.next
    }
    // once end of a list has been reached
    if (l1 !== null) {
        // if it's the end of second list point pointer to rest of l1
        prev.next = l1;
    } else {
        // else point it to the rest of l2
        prev.next = l2;
    }
    return prehead.next;
};
```
### Best Time to Buy and Sell Stock
```golang
func maxProfit(prices []int) int {
    minPrice := int(^uint(0) >> 1)
    maxProfit := 0
    for _, price := range prices {
        if price < minPrice {
            minPrice = price
        } else if price - minPrice > maxProfit {
            maxProfit = price - minPrice
        }
    }
    return maxProfit
}
```

### Valid Palindrome
```typescript
function isPalindrome(s: string): boolean {
    let begin = 0; 
    let end = s.length - 1;
    // have two pointers in the beginning and end
    while (begin < end) {
        // we don't consider non-alphanumeric characters
        // if current char is not a letter or number, move to the next
        while (begin < end && !s[begin].match(/[a-z0-9]/i)) {
            begin++;
        }
        // if current char from the end is not a letter or number, move to the previous char
        while (begin < end && !s[end].match(/[a-z0-9]/i)) {
            end--;
        }
        // if characters from both ends are not equal, not a palindrome
        if(s[begin].toLowerCase() !== s[end].toLowerCase()) return false;
        // move pointer and keep checking
        begin++;
        end--;
    }
    // if never returned while checking it is implied that string is a palindrome
    return true;
};
```

### Invert Binary Tree
Time Complexity: O(n) since each node visited once

Space Complexity: Due to recursion, O(h) function calls will be placed on the stack where h is height of tree. however, h ∈ O(n) so space complexity is also the same.
```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */


function invertTree(root: TreeNode | null): TreeNode | null {
    // if root has subtrees
    if (root != null) {
        // recursively invert left subtree first
        invertTree(root.left);
        // recursively invert right subtree first
        invertTree(root.right);

        // finally invert left and right top level subtrees
        let temp: TreeNode = root.left;
        root.left = root.right;
        root.right = temp;
    }
    return root;
};
```

### Valid Anagram
Time Complexity: O(n) where n is the length of the strings. we go over each string one at a time.

Space Complexity: O(1) since we declare the size of the array and then perform operations on it
```typescript
function isAnagram(s: string, t: string): boolean {
    // anagrams must be on strings of equal length;
    if (s.length !== t.length) {
        return false;
    }
    const charCodeA = 'a'.charCodeAt(0);
    // we use a counter for each alphabet
    // each element represents the position in the alphabet
    const counter: number[] = new Array(26).fill(0);

    // for the first string, increase the frequency at each position
    for (let i = 0; i < s.length; i++) {
        counter[s.charCodeAt(i) - charCodeA]++;
    }

    // for the second string, decrease the frequency at each position
    for (let i = 0; i < t.length; i++) {
        counter[t.charCodeAt(i) - charCodeA]--;
        // for two strings to be anagrams, they should have
        // the same frequency of all letters
        // if the string lengths are the same but have different letters, we will have
        // a negative value and so it'll return out
        if (counter[t.charCodeAt(i) - charCodeA] < 0) {
            return false;
        }
    }
    return true;
}
```
### Binary Search
Time Complexity: O(logn) nums is divided into half each time. In the worst-case scenario, we need to cut nums until the range has no element, and it takes logarithmic time to reach this break condition.

Space Compexity: O(1) since only left, right, and middle are declared.

```typescript
function search(nums: number[], target: number): number {
    let start = 0;
    let end = nums.length - 1;
    
    while (start <= end) {
       let mid = Math.floor((start + end) / 2);
        if (target === nums[mid]) return mid;
        if (target < nums[mid]) {
            end = mid - 1;
        } else if (target > nums[mid]) {
            start = mid + 1;
        }
    }
    return -1; 
};
```

### Flood Fill
Time Complexity: O(n) where n is the maximum number of pixels. we might need to visit each pixel.

Space Complexity: O(n) the size of the call stack during DFS since each pixel visited recursively. 
```typescript
function floodFill(image: number[][], sr: number, sc: number, newColor: number): number[][] {
  // use dfs and hence, use recursion. go all the way to the end.
  // start with getting the original color
  let color = image[sr][sc];
  if (color !== newColor) {
    dfs(image, sr, sc, color, newColor);
  }
  return image;
};

function dfs(image, r, c, color, newColor) {
  // for the first iteration, this will always be true.
  // for subsequent iterations, this refers to a neighboring cell
  // if the neighboring cells are the same color as the original, change the color.
  // also avoids visiting a cell twice if valid
  if (image[r][c] === color) {
    image[r][c] = newColor;
    // then keep traversing row wise until you reach the first row
    if (r - 1 >= 0) dfs(image, r - 1, c, color, newColor);
    // then keep traversing column wise until you reach the first column
    if (c - 1 >= 0) dfs(image, r, c - 1, color, newColor);
    // then keep traversing row wise until you reach last row
    if (r + 1 < image.length) dfs(image, r + 1, c, color, newColor);
    // lastly keep traversing column wise until last column
    if (c + 1 < image[0].length) dfs(image, r, c + 1, color, newColor);
  }
}
```
### Maximum sub-array
#### Brute Force
After the first run, total sum is 1. We see that the max total reached stays at 0 until index 3, and current total is also as 0. Then the current total drops to -1 at index 4, the max total remains 0. At index 5, current total becomes 1, max total becomes 1. At index 6, current total becomes 2, max total (max of current and max) also becomes 2. At the end, the current total never rises above max total.

In the next run starting at index 1, current total restarts at 0. At index 1, current total is 1, max total is 2. No change. Then max current total is -2, max total is 2. Then current and max totals are both 2. Then current total is 1, max total stays 2. Then current total rises to 3 at j=5 and so does max total. Then current total rises to 4 at j=6 and so does max total. Current total then ends at 3.

Restart at index 2. At j=2, current total starts at -3, then rises to 1. Max total remains 4. Then current total drops to 0, then rises to 3. Then drops to 2. Max total never changes.

When you start at index 3. Current total starts at 4, drops to 3, and then rises to 6. Max total also rises to 6. never drops thereafter.

Effectively in each interaction, you're dropping one element in the beginning and finding totals.
```typescript
let arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4];

function maxSubArray(nums: number[]): number {
    let max_subarray = Number.NEGATIVE_INFINITY;
    for(let i = 0; i < nums.length; i++) {
        let current_subarray = 0;
        for (let j = i; j < nums.length; j++) {
            current_subarray += nums[j];
            max_subarray = Math.max(current_subarray, max_subarray);
        }
    }
    return max_subarray;
};
```

#### Kadane's Algorithm (Dynamic Programming)
Brute force gets tweaked. We start with the current and max total at the first element, -2. Then we start at the next index, and check the element with the current total. If the current total would rise when we add the current element to the current total, we assign the current total to be the current element, since only a positive number can do that. The max total count also starts at the current positive element.

Effectively, we drop the previous element. Otherwise, it's assumed that two positive numbers followed each other and the total rose in any case. 

So when i=2, the current total would drop. Our longest subarray sum at this point is the solitary 1. If the array ended here, that would be the answer.

When i=3, the current total rises. We have a positive number. Check if the positive number is bigger than the previous positive number. If yes, we start calculating again from this bigger positive number.The max sub array is just the positive 4.

When i=4, the current total stays the same. The subarray total is positive but has dropped to 3 compared to the standalone 4. 

Then at i=5, another positive number. The current total rises to 5, so the max subarray has also risen to 5.

At i=6, the positive number pushes current and max total again. 

At i=7, the big negative has dropped current total and max total. So we don't do anything. 

At i = 8, the big positive has raised current total once more, but not enough to bump up current and max total.
Meanwhile, the max total is 
```typescript
let arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4];

function maxSubArray(nums: number[]): number {
    let current = nums[0];
    let max = nums[0];
    for (let i = 1; i < nums.length; i++) {
        current = Math.max(nums[i], current + nums[i]);
        max = Math.max(max, current);
    }
    return max;
};
```
