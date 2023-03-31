## Need of the Bitwise Algorithms :-

- Space Efficiency
- Time Efficiency
- Masking and Bitwise Encoding
- Optimization
- Hardware Interaction

### Concept of mask

By shifting 1 to desired postion we can create mask to perform certain operations

```cpp
mask = 1 >> position;
```

### 1U

1U means 1 in binary form as unsigned integer
The expression `(1U << n) - 1` gives a number that contains last n bits set and other bits as 0.
for example: `(1U << 4) -1` is `0000 1111` in 8bit binary

> as `(1U << 4)` is `0001 0000`

### Two's compliment

`-n` or `~(n-1)` both gives twos compliemnt of a number
`~(n-1)` is equivalent to `-n (minus n)`

### 1. How to Set a bit in the number?

use the “OR” operator with mask to set the bit at that position.

```cpp
#include <iostream>
using namespace std;

int main(){
  int num = 4, pos = 1;
  int mask = (1 << pos);
  num = num | mask;
  cout<<num<<endl;
  return 0;
}

```

### 2. How to unset/clear a bit at n’th position in the number

we use bitwise NOT operator ‘~’ with mask to unset this shifted ‘1’.
Resulting in say, `11111110111111` type of mask
we will ‘AND'(&) with the number ‘num’ that will unset bit at nth position.

```cpp
#include <iostream>
using namespace std;

int main(){
  int num = 4, pos = 1;
  int mask = ~(1 << pos);
  num = num & mask;
  cout<<num<<endl;
  return 0;
}

```

### 3. Toggling a bit at nth position

we will XOR with the mask that will toogle bit at nth position.

`1^x== (0, if x==1) and (1, if x==0)`

```cpp
#include <iostream>
using namespace std;

int main(){
  int num = 4, pos = 1;
  int mask = (1 << pos);
  num = num ^ mask;
  cout<<num<<endl;
  return 0;
}

```

### 4. Checking if the bit at nth position is Set or Unset

we will AND with mask, if it is 0, bit in unset

```cpp
#include <iostream>
using namespace std;

int main(){
  int num = 4, pos = 1;
  int mask = (1 << pos);
  bool bit = num & mask;
  cout<<bit<<endl;
  return 0;
}

```

### 5. Multiply a number by 2 using the left shift operator

```cpp
#include <iostream>
using namespace std;

int main(){
  int num = 4;
  int ans = num<<1;
  cout<<ans<<endl;
  return 0;
}

```

### 6. Divide a number 2 using the right shift operator

```cpp
#include <iostream>
using namespace std;

int main(){
  int num = 4;
  int ans = num>>1;
  cout<<ans<<endl;
  return 0;
}

```

### Count the number of ones in the binary representation of the given number

Here `n-1` unset rightmost set bit and set all the bits in right to that, which upon AND with n clears that rightmost set bit

n = `0011 0100`
n-1 = `0011 0011`
n&(n-1) = `0011 0000`

```cpp
int count_one(int n) {
    while(n) {
        n = n&(n-1);
        count++;
    }
    return count;
}
```

### 7. Compute XOR from 1 to n (direct method)

It is obeserved that XOR follows some pattern in interval of 4.

`If Remainder is 0 XOR will be n, for remainder 1 XOR will be 1, for remainder 2 XOR will be n+1, for remainder 3 XOR will be 0.`

```cpp
// C++ program to find XOR of numbers from 1 to n.
int computeXOR(int n){
if (n % 4 == 0) return n;
if (n % 4 == 1) return 1;
if (n % 4 == 2) return n + 1;
return 0;
}

```

### 8. How to know if a number is a power of 2?

If a number is power of 2, it will be like `0001 0000` so only one bit will be set.
If we substract 1 from this number, result will be `0000 1111` so, now if we take AND of both numbers it will come out as 0 (because n was power of 2)
Otherwise let say number `0101 0000`, substracting 1 will be give `0100 1111` which upon AND gives `0100 0000` which is not 0.

` We will have to check for 0 separately`

```cpp
bool isPowerOfTwo(int n){
// n&& is for case where n is 0
return n && (!(n&(n-1)));
}

```

### Is power of four

`!(n&(n-1))` this checks if only one bit is set, if it is zero that means only `1 bit` is set in `n`.
`0x55555555` is `0b1010101010101010101010101010101` in binary
so, if `n&0x55555555` is non zero that means some position has set bit which contributes to power of 4.

```cpp
bool isPowerOfFour(int n) {
    return !(n&(n-1)) && (n&0x55555555);
    //check the 1-bit location;
}
```

### 9. Count Set bits in an integer

Check all bits individually by using AND

```cpp
int countBits(int n){
  int count = 0;
  while (n) {
    count += n & 1;
    n >>= 1;
  }
  return count;
}


```

### 10. Position of rightmost set bit

`~(n-1) is equivalent to -n (minus n)`

`(n&~(n-1))` or `n&-n` always return the number containing the rightmost set bit as 1.

Bitwise AND of n and it's 2's compliment gives number with only set bit as rightmost set bit of original number
`n&-n` gives the number with rightmost set bit

> Example in 8 bit numbers

Say n is `0010 0100`
`(n-1)` will be `0010 0011`, `~(n-1)` will be `1101 1100`
It can be noticed between `0010 0100` and `1101 1100` that position of first set bit is set in both numbers (other bits are different) so by taking and, we can take log2 to find position.

```cpp
// C program for Position
// of rightmost set bit
#include <math.h>
#include <stdio.h>

// Driver code
int main()
{
  int n = 18;
  // -n is equivalent to ~(n-1)
  int ans = log2(n & -n) + 1;
  return 0;
}

```

```cpp
int positionOfRightmostSetBit(int n)
{
  if (n & 1) return 1;

  // unset rightmost bit and xor with the number itself
  n = n ^ (n & (n - 1));

  // find the position of the only set bit in the result;
  // we can directly return `log2(n) + 1` from the
  // function
  int pos = 0;
  while (n) {
    n = n >> 1;
    pos++;
  }
  return pos;
}


```

> Different approach can be followed based on these intutions

### Count number of bits to be flipped to convert A to B

<p><strong class="example">Approach</strong></p>

- Check bits individually by comparing them

OR

- Take XOR of both numbers and count total set bits (XOR will make different bits as set.)

```cpp
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that count set bits
int countSetBits(int n){
  int count = 0;
  while (n > 0) {
    count++;
    n &= (n - 1);
  }
  return count;
}

int FlippedCount(int a, int b){
  return countSetBits(a ^ b);
}



```

### Swap bits in a given number

> Given a number x and two positions (from the right side) in the binary representation of x, write a function that swaps n bits at the given two positions and returns the result. It is also given that the two sets of bits do not overlap.

`Inputs : Number, Position 1, Position 2, Number of bits to be swapped`

<p><strong class="example">Approach</strong></p>

Here the idea is to create two numbers `set1` and `set2` which will contains only bits which is to be swapped. Then we will take XOR of both numbers, and shift it accordingly to positions and create a final number. XORing with this final number, bits will be swapped

Steps:

- Move all bits of the first set to the rightmost side
  `set1 =  (x >> p1) & ((1U << n) - 1)`
  > Here the expression (1U << n) - 1 gives a number that contains last n bits set and other bits as 0. We do & with this expression so that bits other than the last n bits become 0.
- Move all bits of second set to rightmost side
  `set2 =  (x >> p2) & ((1U << n) - 1)`
- XOR the two sets of bits
  `xor = (set1 ^ set2) `
- Put the xor bits back to their original positions.
  `xor = (xor << p1) | (xor << p2)`
- Finally, XOR the xor with original number so that the two sets are swapped.
  `result = x ^ xor`

#### Here is an example to visualise.

Number = `0100 {pos2, 4bits} 0010 {pos1, 4bits} 0010`

> In bracket variables represent 4 bits

set1 = `0000 0000 0000 0000 {pos1}`
set2 = `0000 0000 0000 0000 {pos2}`
xor = `0000 0000 0000 0000 {pos1^pos2}`

> `xor = (xor << p1) | (xor << p2)` is equivalent to

xor = `0000 {pos1^pos2} 0000 {pos1^pos2} 0000`
Number = `0100 {pos2} 0010 {pos1} 0010`

> visualise 4 bit as individual block, so XOR with 0 will remain unaffected, and XOR of `pos2` with `{pos1^pos2}` is `pos2^pos1^pos2` which is equivalent to pos1 and so.

Answer = `0100 {pos1} 0010 {pos2} 0010`

> Same as swapping two numbers.

```cpp
// C++ Program to swap bits
// in a given number
#include <bits/stdc++.h>
using namespace std;

int swapBits(unsigned int x, unsigned int p1,
unsigned int p2, unsigned int n)
  {
  unsigned int set1 = (x >> p1) & ((1U << n) - 1);
  unsigned int set2 = (x >> p2) & ((1U << n) - 1);

  unsigned int Xor = (set1 ^ set2);

  /* Put the Xor bits back to their original positions */
  Xor = (Xor << p1) | (Xor << p2);

  /* Xor the 'Xor' with the original number so that the
  two sets are swapped */
  unsigned int result = x ^ Xor;

  return result;
}

```

### Detect if two integers have opposite signs

Positive number has Left most bit MSB as `0` while negative number has MSB as `1`, so if we `XOR` both numbers and the result has MSB bit as `1` that means that MSB bit was different for both numbers, so they have oppositie signs

```cpp
bool oppositeSigns(int x, int y){
  return (x < 0)? (y >= 0): (y < 0);
}
```

### 7. The Quickest way to swap two numbers:

```cpp
#include <iostream>
using namespace std;

int main(){
  int a = 5;
  int b = 7;
  cout<<"Before Swapping, a = "<<a<<" "<<"b = "<<b<<endl;
  a ^= b;
  b ^= a;
  a ^= b;
  cout<<"After Swapping, a = "<<a<<" "<<"b = "<<b<<endl;
  return 0;
}

```

### Given a set, find XOR of the XOR’s of all subsets.

> The question is to find XOR of the XOR’s of all subsets. i.e if the set is {1,2,3}. All subsets are : [{1}, {2}, {3}, {1, 2}, {1, 3}, {2, 3}, {1, 2, 3}]. Find the XOR of each of the subset and then find the XOR of every subset result.

- Let us consider n’th element, it can be included in the power set of remaining (n-1) elements. The number of subsets for (n-1) elements is equal to 2(n-1) which is always even when n>1. Thus, in the XOR result, every element is included even number of times and XOR of even occurrences of any number is 0.

```cpp
int findXOR(int Set[], int n){
  if(n == 1) return Set[0];
  return 0;
}
```

### Find the number of leading, trailing zeroes and number of 1’s

We can quickly find the number of leading, trailing zeroes and number of 1’s in a binary code of an integer in C++ using GCC.
It can be done by using inbuilt functions i.e.

```
Number of leading zeroes: __builtin_clz(x)
Number of trailing zeroes : __builtin_ctz(x)
Number of 1-bits: __builtin_popcount(x)
```

<p>Refer<a href="https://www.geeksforgeeks.org/builtin-functions-gcc-compiler/"> GCC inbuilt functions</a> for details.</p>

### Equal Sum and XOR

> Count of numbers (x) smaller than or equal to n such that n+x = n^x

We know that `(n+i)=(n^i) + ((n&i)<<1)` i.e., sum of number without carry and carry (shifted by 1) which is sum of XOR and sum of AND shfited by 1 bit.
Or, `(n+i)=(n^i)+ 2*(n&i)` left shifting is equivalent to multiplying with 2.
We wants `i` which satisfies `(n+i)=(n^i)` so that means we want `i` such that `(n&i)==0`
Since we want count, we can take number of bits which are unset in n (that only will contribute the AND result in 0) and form all possible combinations, which will be equal to `2 to the power unset_bits`

```cpp

#include <iostream>
using namespace std;

int main()
{
    int n=453,unset_bitcount=0;
    while(n){
        if(n&1==0) unset_bitcount++;
        n>>=1;
    }
    // equivalent to 2^unset_bitcount
    return 1<<unset_bitcount;
}

```

### Missing Number

> Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array. For example, Given nums = [0, 1, 3] return 2. (Of course, you can do this by math.)

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int ans=nums.size();
        for(int i=0;i<nums.size();i++) ans^=nums[i]^i;
        return ans;
    }
};
```

### Add two numbers without using arithmetic operators

XOR will give sum of numbes without considering carry, so we will shift carry by 1 and then again add it with sun until carry becomes 0;

```cpp

int Add(int x, int y){
  while (y != 0){
    unsigned carry = x & y;
    x = x ^ y;
    y = carry << 1;
  }
  return x;
}
```

```cpp
class Solution {
public:
    int getSum(int a, int b) {
        // for adding two numbers, XOR operation can give result of current position
        // and AND operation gives carry for that following position
        // the good thing is that, we do not need to do these things bit by bit
        // we can perform XOR operation on complete binary digits
        // and then add the carry part (ofcourse shifted by 1 bit)
        // using same operation until cary becomes zero
        // https://www.youtube.com/watch?v=gVUrDV4tZfY
        while(b!=0){
            // here unsigned int is taken because by left shifting, number can get negative
            int temp=(unsigned int)(a&b)<<1;
            a=a^b;
            b=temp;
        }
        return a;
    }
};
```

```cpp
int getSum(int a, int b) {
    return b==0? a:getSum(a^b, (a&b)<<1); //be careful about the terminating condition;
}
```

### Find the element that appears once

Here if we will XOR all elements of array, duplicate elements will cancel each other and we will be left with unique element appearing only once.

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int result = nums[0];
        for(int i=1;i<nums.size();i++) result=result^nums[i];
        return result;
    }
};
```

### Leetcode 260. Single Number III

<p>Given an integer array <code>nums</code>, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once. You can return the answer in <strong>any order</strong>.</p>

<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,1,3,2,5]
<strong>Output:</strong> [3,5]
<strong>Explanation: </strong> [5, 3] is also a valid answer.
</pre>

<p><strong class="example">Approach</strong></p>

- The idea is to divide the numbers in two groups on basis of differing bits in the two elements appearing once.
- Here we will find XOR all numbers which will give result as XOR of a^b (numbers occuring only once).
- In the resultant number first set bit will be the bit which will differ in both numbers
  > Example a =`0010` b = `1000` XOR = `1010`
  > first different bit in `a` and `b` is second bit, so in XOR rightmost set bit is `2nd`
- Find out a number with only set bit as rightmost set bit (bit which is different in both numbers)

```cpp
bit_which_differs_in_both_a_b_rightmost = XOR&(~(XOR-1));
// OR
bit_which_differs_in_both_a_b_rightmost = XOR&(-XOR);
```

- Divide all numbers in 2 groups based on `only set bit` calculated above, so a in come in one group and b in other.

- XOR within groups to find out a and b

```cpp
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        if(nums.size()<3) return nums;
        vector<int> answer;
        // METHOD - 1 USING MAPS

        unordered_map<int,int> m;
        for(int num:nums) m[num]++;
        for(auto e:m) if(e.second==1) answer.push_back(e.first);
        // END OF METHOD 1

        return answer;
    }
};
```

```cpp
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        if(nums.size()<3) return nums;
        vector<int> answer;

        // METHOD - 2 USING SORTING ALGORITHIMS

        sort(nums.begin(),nums.end());
        int i=0,n=nums.size()-1;
        if(nums[0]!=nums[1]) answer.push_back(nums[i++]);
        if(nums[n]!=nums[n-1]) answer.push_back(nums[n]);
        if(answer.size()==2) return answer;
        while(i<n){
            if(nums[i]==nums[i+1]) i+=2;
            else{
                answer.push_back(nums[i]);
                i++;
            }
        }
        // END OF METHOD 2

        return answer;
    }
};
```

`Important`

```cpp
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        if(nums.size()<3) return nums;
        vector<int> answer;

        // METHOD - 3 USING BIT MANIPULTAION
        unsigned int differ_bit=0;
        for(auto num:nums) differ_bit^=num;
        differ_bit = differ_bit & (-differ_bit);
        int group_1=0,group_2=0;
        for(auto num:nums){
            if(differ_bit&num) group_1^=num;
            else group_2^=num;
        }
        answer.push_back(group_1);
        answer.push_back(group_2);
        // END OF METHOD 2

        return answer;
    }
};
```
