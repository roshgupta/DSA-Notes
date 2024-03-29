<div class="break-words"><div><div class="_16yfq _2YoR3"><h3 id="wiki">Wiki</h3>
<p>Bit manipulation is the act of algorithmically manipulating bits or other pieces of data shorter than a word. Computer programming tasks that require bit manipulation include low-level device control, error detection and correction algorithms, data compression, encryption algorithms, and optimization. For most other tasks, modern programming languages allow the programmer to work directly with abstractions instead of bits that represent those abstractions. Source code that does bit manipulation makes use of the bitwise operations: AND, OR, XOR, NOT, and bit shifts.</p>
<p>Bit manipulation, in some cases, can obviate or reduce the need to loop over a data structure and can give many-fold speed ups, as bit manipulations are processed in parallel, but the code can become more difficult to write and maintain.</p>
<h3 id="details">Details</h3>
<h4 id="basics">Basics</h4>
<p>At the heart of bit manipulation are the bit-wise operators &amp; (and), | (or), ~ (not) and ^ (exclusive-or, xor) and shift operators a &lt;&lt; b and a &gt;&gt; b.</p>
<blockquote>
<p>There is no boolean operator counterpart to bitwise exclusive-or, but there is a simple explanation. The exclusive-or operation takes two inputs and returns a 1 if either one or the other of the inputs is a 1, but not if both are. That is, if both inputs are 1 or both inputs are 0, it returns 0. Bitwise exclusive-or, with the operator of a caret, ^, performs the exclusive-or operation on each pair of bits. Exclusive-or is commonly abbreviated XOR.</p>
</blockquote>
<ul>
<li>Set union A | B</li>
<li>Set intersection A &amp; B</li>
<li>Set subtraction A &amp; ~B</li>
<li>Set negation ALL_BITS ^ A or ~A</li>
<li>Set bit A |= 1 &lt;&lt; bit</li>
<li>Clear bit A &amp;= ~(1 &lt;&lt; bit)</li>
<li>Test bit (A &amp; 1 &lt;&lt; bit) != 0</li>
<li>Extract last bit A&amp;-A or A&amp;~(A-1) or x^(x&amp;(x-1))</li>
<li>Remove last bit A&amp;(A-1)</li>
<li>Get all 1-bits ~0</li>
</ul>
<h4 id="examples">Examples</h4>
<p>Count the number of ones in the binary representation of the given number</p>

```cpp
int count_one(int n) {
    while(n) {
        n = n&(n-1);
        count++;
    }
    return count;
}
```

<p>Is power of four (actually map-checking, iterative and recursive methods can do the same)</p>

```cpp
bool isPowerOfFour(int n) {
    return !(n&(n-1)) && (n&0x55555555);
    //check the 1-bit location;
}
```

<h4 id="-tricks"><code>^</code> tricks</h4>
<p>Use <code>^</code> to remove even exactly same numbers and save the odd, or save the distinct bits and remove the same.</p>
<h5 id="sum-of-two-integers">Sum of Two Integers</h5>
<p>Use <code>^</code> and <code>&amp;</code> to add two integers</p>

```cpp
int getSum(int a, int b) {
    return b==0? a:getSum(a^b, (a&b)<<1); //be careful about the terminating condition;
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
	
	

<h5 id="missing-number">Missing Number</h5>
<p>Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.  For example, Given nums = [0, 1, 3] return 2. (Of course, you can do this by math.)</p>

```cpp
int missingNumber(vector<int>& nums) {
    int ret = 0;
    for(int i = 0; i < nums.size(); ++i) {
        ret ^= i;
        ret ^= nums[i];
    }
    return ret^=nums.size();
}
```

<h4 id="-tricks-1"><code>|</code> tricks</h4>
<p>Keep as many 1-bits as possible</p>
<p>Find the largest power of 2 (most significant bit in binary form), which is less than or equal to the given number N.</p>

```cpp
long largest_power(long N) {
    //changing all right side bits to 1.
    N = N | (N>>1);
    N = N | (N>>2);
    N = N | (N>>4);
    N = N | (N>>8);
    N = N | (N>>16);
    return (N+1)>>1;
}
```

<h5 id="reverse-bits">Reverse Bits</h5>
<p>Reverse bits of a given 32 bits unsigned integer.</p>
<h6 id="solution">Solution</h6>

```cpp
uint32_t reverseBits(uint32_t n) {
    unsigned int mask = 1<<31, res = 0;
    for(int i = 0; i < 32; ++i) {
        if(n & 1) res |= mask;
        mask >>= 1;
        n >>= 1;
    }
    return res;
}
```

```cpp
uint32_t reverseBits(uint32_t n) {
	uint32_t mask = 1, ret = 0;
	for(int i = 0; i < 32; ++i){
		ret <<= 1;
		if(mask & n) ret |= 1;
		mask <<= 1;
	}
	return ret;
}
```

<h4 id="-tricks-2"><code>&amp;</code> tricks</h4>
<p>Just selecting certain bits</p>
<p>Reversing the bits in integer</p>

```
x = ((x & 0xaaaaaaaa) >> 1) | ((x & 0x55555555) << 1);
x = ((x & 0xcccccccc) >> 2) | ((x & 0x33333333) << 2);
x = ((x & 0xf0f0f0f0) >> 4) | ((x & 0x0f0f0f0f) << 4);
x = ((x & 0xff00ff00) >> 8) | ((x & 0x00ff00ff) << 8);
x = ((x & 0xffff0000) >> 16) | ((x & 0x0000ffff) << 16);
```

<h5 id="bitwise-and-of-numbers-range">Bitwise AND of Numbers Range</h5>
<p>Given a range [m, n] where 0 &lt;= m &lt;= n &lt;= 2147483647, return the bitwise AND of all numbers in this range, inclusive.  For example, given the range [5, 7], you should return 4.</p>
<h6 id="solution-1">Solution</h6>

```cpp
int rangeBitwiseAnd(int m, int n) {
    int a = 0;
    while(m != n) {
        m >>= 1;
        n >>= 1;
        a++;
    }
    return m<<a;
}
```

<h5 id="number-of-1-bits">Number of 1 Bits</h5>
<p>Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).</p>
<h6 id="solution-2">Solution</h6>

```cpp
int hammingWeight(uint32_t n) {
	int count = 0;
	while(n) {
		n = n&(n-1);
		count++;
	}
	return count;
}
```

```cpp
int hammingWeight(uint32_t n) {
    ulong mask = 1;
    int count = 0;
    for(int i = 0; i < 32; ++i){ //31 will not do, delicate;
        if(mask & n) count++;
        mask <<= 1;
    }
    return count;
}
```

<h4 id="application">Application</h4>
<h5 id="repeated-dna-sequences">Repeated DNA Sequences</h5>
<p>All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.  Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.<br>
For example,<br>
Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",<br>
Return: ["AAAAACCCCC", "CCCCCAAAAA"].</p>
<h6 id="solution-3">Solution</h6>

```cpp
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        int sLen = s.length();
        vector<string> v;
        if(sLen < 11) return v;
        char keyMap[1<<21]{0};
        int hashKey = 0;
        for(int i = 0; i < 9; ++i) hashKey = (hashKey<<2) | (s[i]-'A'+1)%5;
        for(int i = 9; i < sLen; ++i) {
            if(keyMap[hashKey = ((hashKey<<2)|(s[i]-'A'+1)%5)&0xfffff]++ == 1)
                v.push_back(s.substr(i-9, 10));
        }
        return v;
    }
};
```

<blockquote>
<p>But the above solution can be invalid when repeated sequence appears too many times, in which case we should use <code>unordered_map&lt;int, int&gt; keyMap</code> to replace <code>char keyMap[1&lt;&lt;21]{0}</code>here.</p>
</blockquote>
<h5 id="majority-element">Majority Element</h5>
<p>Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times. (bit-counting as a usual way, but here we actually also can adopt sorting and Moore Voting Algorithm)</p>
<h6 id="solution-4">Solution</h6>

```cpp
int majorityElement(vector<int>& nums) {
    int len = sizeof(int)*8, size = nums.size();
    int count = 0, mask = 1, ret = 0;
    for(int i = 0; i < len; ++i) {
        count = 0;
        for(int j = 0; j < size; ++j)
            if(mask & nums[j]) count++;
        if(count > size/2) ret |= mask;
        mask <<= 1;
    }
    return ret;
}
```

<h5 id="single-number-iii">Single Number III</h5>
<p>Given an array of integers, every element appears three times except for one. Find that single one. (Still this type can be solved by bit-counting easily.) But we are going to solve it by <code>digital logic design</code></p>
<h6 id="solution-5">Solution</h6>

```cpp
//inspired by logical circuit design and boolean algebra;
//counter - unit of 3;
//current   incoming  next
//a b            c    a b
//0 0            0    0 0
//0 1            0    0 1
//1 0            0    1 0
//0 0            1    0 1
//0 1            1    1 0
//1 0            1    0 0
//a = a&~b&~c + ~a&b&c;
//b = ~a&b&~c + ~a&~b&c;
//return a|b since the single number can appear once or twice;
int singleNumber(vector<int>& nums) {
    int t = 0, a = 0, b = 0;
    for(int i = 0; i < nums.size(); ++i) {
        t = (a&~b&~nums[i]) | (~a&b&nums[i]);
        b = (~a&b&~nums[i]) | (~a&~b&nums[i]);
        a = t;
    }
    return a | b;
}
;
```

<h5 id="maximum-product-of-word-lengths">Maximum Product of Word Lengths</h5>
<p>Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.</p>
<blockquote>
<p>Example 1:<br>
Given ["abcw", "baz", "foo", "bar", "xtfn", "abcdef"]<br>
Return 16<br>
The two words can be "abcw", "xtfn".</p>
</blockquote>
<blockquote>
<p>Example 2:<br>
Given ["a", "ab", "abc", "d", "cd", "bcd", "abcd"]<br>
Return 4<br>
The two words can be "ab", "cd".</p>
</blockquote>
<blockquote>
<p>Example 3:<br>
Given ["a", "aa", "aaa", "aaaa"]<br>
Return 0<br>
No such pair of words.</p>
</blockquote>
<h6 id="solution-6">Solution</h6>
<p>Since we are going to use the length of the word very frequently and we are to compare the letters of two words checking whether they have some letters in common:</p>
<ul>
<li>using an array of int to pre-store the length of each word reducing the frequently <em>measuring</em> process;</li>
<li>since int has 4 bytes, a 32-bit type, and there are only 26 different letters, so we can just use one bit to indicate the existence of the letter in a word.</li>
</ul>

```cpp
int maxProduct(vector<string>& words) {
    vector<int> mask(words.size());
    vector<int> lens(words.size());
    for(int i = 0; i < words.size(); ++i) lens[i] = words[i].length();
    int result = 0;
    for (int i=0; i<words.size(); ++i) {
        for (char c : words[i])
            mask[i] |= 1 << (c - 'a');
        for (int j=0; j<i; ++j)
            if (!(mask[i] & mask[j]))
                result = max(result, lens[i]*lens[j]);
    }
    return result;
}
```

<h4 id="attention">Attention</h4>
<ul>
<li>result after shifting left(or right) too much is undefined</li>
<li>right shifting operations on negative values are undefined</li>
<li>right operand in shifting should be non-negative, otherwise the result is undefined</li>
<li>The &amp; and | operators have lower precedence than comparison operators</li>
</ul>
<h3 id="sets">Sets</h3>
<p>All the subsets<br>
A big advantage of bit manipulation is that it is trivial to iterate over all the subsets of an N-element set: every N-bit value represents some subset. Even better, <code>if A is a subset of B then the number representing A is less than that representing B</code>, which is convenient for some dynamic programming solutions.</p>
<p>It is also possible to iterate over all the subsets of a particular subset (represented by a bit pattern), provided that you don’t mind visiting them in reverse order (if this is problematic, put them in a list as they’re generated, then walk the list backwards). The trick is similar to that for finding the lowest bit in a number. If we subtract 1 from a subset, then the lowest set element is cleared, and every lower element is set. However, we only want to set those lower elements that are in the superset. So the iteration step is just <code>i = (i - 1) &amp; superset</code>.</p>

```cpp
vector<vector<int>> subsets(vector<int>& nums) {
    vector<vector<int>> vv;
    int size = nums.size();
    if(size == 0) return vv;
    int num = 1 << size;
    vv.resize(num);
    for(int i = 0; i < num; ++i) {
        for(int j = 0; j < size; ++j)
            if((1<<j) & i) vv[i].push_back(nums[j]);
    }
    return vv;
}
```

<p>Actually there are two more methods to handle this using <code>recursion</code> and <code>iteration</code> respectively.</p>
<h3 id="bitset">Bitset</h3>
<p>A <a href="http://www.cplusplus.com/reference/bitset/bitset/?kw=bitset" target="_blank">bitset</a> stores bits (elements with only two possible values: 0 or 1, true or false, ...).<br>
The class emulates an array of bool elements, but optimized for space allocation: generally, each element occupies only one bit (which, on most systems, is eight times less than the smallest elemental type: char).</p>

```cpp
// bitset::count
#include <iostream>       // std::cout
#include <string>         // std::string
#include <bitset>         // std::bitset

int main () {
  std::bitset<8> foo (std::string("10110011"));
  std::cout << foo << " has ";
  std::cout << foo.count() << " ones and ";
  std::cout << (foo.size()-foo.count()) << " zeros.\n";
  return 0;
}
```

<p>Always welcom new ideas and <code>practical</code> tricks, just leave them in the comments!</p></div></div></div>
