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