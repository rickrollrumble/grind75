# Grind 75
## Week 3
### Ransom Note
Time Complexity: O(m). Creating a counter for m characters in magazine takes O(m) time and O(1) for an insert or update. Then O(n) time for going through ransom note and O(1) for lookup. m > n, so O(m) is the worst case time.

Space Complexity: O(1), the map will never have more than 26 characters.
```typescript
function canConstruct(ransomNote: string, magazine: string): boolean {
  // in obvious case, if ransom note has more letters it cannot be constructed from magazine
  if (ransomNote.length > magazine.length) return false;
  // initialize a letter count map
  let mag = {}
  for (let c of magazine) {
    // if letter already exists, increment count.
    // if it doesn't, initialize count.
    mag[c] = (mag[c] || 0) + 1;
  }  

  for(let c of ransomNote) {
    // if letter doesn't exist in map, return false.
    // if it does, decrease the count in the map.
    // for any additional count of letters, the count will decrease
    // to less than zero.
    if(!mag[c] || mag[c] <= 0) return false;
    mag[c]--;
  }
  return true;
};
```
