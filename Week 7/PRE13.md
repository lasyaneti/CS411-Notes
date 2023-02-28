# PRE13: hash tables 

## Secondary Storage Hash Table
- Every block of memory is hashed 
- Uses overflow blocks when needed 
- Array has fixed length 

### Searching 
1. compute h(a) to get key 
2. get access to bucket by going to array at key

### Insert 
1. hash it 
2. go to block
3. insert if space, else add overflow bucket (linked list)

**want to minimize len of these overflow linked list by using an efficient hash function, else performance decreases significantly**

## Extensible Hash Table 
- Instead of overflow bucket, use an array of pointers, increase array size by x2 whenever space needed
- Array is of size $2^i$
- Only use `i` leftmost bits to index inputs 
- No overflows! 

### Insertion
- if `i > j`, split data block and rearrange
![](/assets/pre13-2.jpg)

- if `j == i`, increase array size by x2 
![](/assets/pre13-1.jpg)

### Performance 
- No overflow buckets, nice! 
- BUT extensions can be **costly and disruptive**
- Extension bucket table may no longer fit in memory! 
- $2^i$ increase rate is realllyyyy big 

## Linear Hash Table 
- Add only 1 bucket at a time (instead of x2)
- h(k) computes `i` which will be rightmost bits 
- If last `i` bits represent m, which is < n, then store into m 
- If m >= n, flip most significant bit 
- Allows overflow blocks  

![](/assets/pre13-3.jpg)

### Insertion 
1. Computer average record per bucket (`r/N`)
2. If still below threshold, add overflow bucket if needed
3. If above threshold, add a new bucket 
    - don't have to go over all blocks to rearrange, only go to newly added buckets, flip most significant bit (within right most range `i`) and rearrange any overflow at that index 

![](/assets/pre13-4.jpg)