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