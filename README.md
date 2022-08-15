- [Recursion](https://github.com/roshgupta/DSA-Notes#recursion)
  - [Print all Sub-Sequences](https://github.com/roshgupta/DSA-Notes#print-all-sub-sequences)
  - [Print all Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#print-all-sub-sequences-with-sum-equals-to-k)
  - [Print ONE Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#print-one-sub-sequences-with-sum-equals-to-k)
  - [Count number of Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#count-number-of-sub-sequences-with-sum-equals-to-k)
- [Bit Manipulation](https://github.com/roshgupta/DSA-Question-Notes#bit-manipulation)
  - [Odd-even number](https://github.com/roshgupta/DSA-Question-Notes#odd-even-number)
  - [Swap two numbers](https://github.com/roshgupta/DSA-Question-Notes#swap-two-numbers)
  - [Bit Masking](https://github.com/roshgupta/DSA-Question-Notes#bit-masking)
  - [XOR Problems](https://github.com/roshgupta/DSA-Question-Notes#xor-problems)
- [Dynamic Programming (DP)](https://github.com/roshgupta/DSA-Question-Notes#dynamic-programming-dp)
  


<hr>

# Recursion

## Print all Sub-Sequences

```cpp
#include <bits/stdc++.h>
using namespace std;
void printSubSequence(int index, int arr[], int n, vector<int> &answer) {
  if (index == n) {
    for (auto it : answer) cout << it << " ";
    if (answer.size() == 0) cout << "{}";
    cout << endl;
    return;
  }
  // pick
  answer.push_back(arr[index]);
  printSubSequence(index + 1, arr, 3, answer);
  // not pick
  answer.pop_back();
  printSubSequence(index + 1, arr, 3, answer);
}

int main() {
  int arr[] = {1, 2, 3};
  vector<int> answer;
  printSubSequence(0, arr, 3, answer);
  return 0;
}


```

## Print all Sub-Sequences with sum equals to K

```cpp


#include <bits/stdc++.h>
using namespace std;
void printS(int ind, vector<int> &ds, int s, int K, int arr[], int n) {
  if (ind == n) {
    if (s == K) {
      for (auto it : ds)
        cout << it << " ";
      cout << endl;
    }
    return;
  }

  ds.push_back(arr[ind]);
  s += arr[ind];
  printS(ind + 1, ds, s, K, arr, n);
  s -= arr[ind];
  ds.pop_back();
  printS(ind + 1, ds, s, K, arr, n);
}

int main() {
  int arr[] = {1, 2, 1};
  int n = 3;
  int K = 2;
  vector<int> ds;
  printS(0, ds, 0, K, arr, n);
  return 0;
}

```

` If we have to print only one sub-sequence then, we can use a boolean flag (which is not advisable). `

OR

## Print ONE Sub-Sequences with sum equals to K

` modifying above code `

```cpp

#include <bits/stdc++.h>
using namespace std;
bool printS(int ind, vector<int> &ds, int s, int K, int arr[], int n) {
  if (ind == n) {
    if (s == K) {
      for (auto it : ds)
        cout << it << " ";
      cout << endl;
      return true;
    }
    return false;
  }

  ds.push_back(arr[ind]);
  s += arr[ind];
  if (printS(ind + 1, ds, s, K, arr, n)) return true;
  s -= arr[ind];
  ds.pop_back();
  if (printS(ind + 1, ds, s, K, arr, n)) return true;
  return false;
}

int main() {
  int arr[] = {1, 2, 1};
  int n = 3;
  int K = 2;
  vector<int> ds;
  printS(0, ds, 0, K, arr, n);
  return 0;
}


```
> here, if any sub sequence is printed, we will return true.
> as soon as a true is returned, further calls will not be made, since it checks for returned value and calls next function only if the returned value is false.

` if we have to count the number of sub-sequences, then we do not have to carry vector array (storing sub-sequences). `

## Count number of Sub-Sequences with sum equals to K

```cpp
#include <bits/stdc++.h>
using namespace std;
int printS(int ind, int s, int K, int arr[], int n) {
  if (ind == n) {
    if (s == K) {
      return 1;
    }
    return 0;
  }
  s += arr[ind];
  int pick = printS(ind + 1, s, K, arr, n);
  s -= arr[ind];
  int notPick = printS(ind + 1, s, K, arr, n);
  return pick + notPick;
}

int main() {
  int arr[] = {1, 2, 1};
  int n = 3;
  int K = 2;
  cout << printS(0, 0, K, arr, n) << endl;
  return 0;
}


```

> In case of counting subsequences, we can return 1 (if condition is satisfied) or, we can return 0. And we will take sum of all returned value.


<!-- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  -->

# Bit Manipulation

<p align="center"><img src="https://images.velog.io/images/gtfo/post/7ec51a46-0ca1-45bc-b39c-efb68848d367/types-of-bitwise-operators.jpg" height="250"></p>

## Odd-even number

> Number & 1 = 0  --> Even <br>
> Number & 1 = 1  --> Odd
```cpp
bool isEven(int a) {
        return !(a & 1);
    }
```

## Swap two numbers

```cpp
 void swap(int a, int b) {
        cout<<"a="<<a<<" "<<"b="<<b<<endl;
        a = a ^ b;
        b = a ^ b;
        a = a ^ b;
        cout<<"a="<<a<<" "<<"b="<<b<<endl;
    }
```

## Bit Masking

### Get ith bit of a number

```cpp
// ith bit of an integer a (LSB to MSB)
    int ithbit(int a, int i) {
        int mask = 1 << i; // left shift 1 by i bits (to the ith bit)

        // ith bit = if (a & mask == 1) 1 else 0
        return a & mask;
    }
```

### Set ith bit of a number

```cpp
// set => set to 1 (by default)
    int setithBit(int a, int i) {
        int mask = 1 << i; // 1 shifted left by i bits

        return a | mask; // will set ith bit
    }
```

### Clear ith bit of a number

```cpp
int clearithBit(int a, int i) {
        int mask = ~(1 << i); // 0 shifted left by i bits (other bits 1)

        return a & mask; // will clear ith bit
    }
```

### Find number of bits to change to convert a to b

```cpp
int differentBits(int a, int b) {
        int t = a ^ b; // XOR will set bits in t where a and b have different bits

        // our answer is the number of set bits in t
        int res = 0;
        /*
        // right shift and increase counter if LSB is 1
        // Time complexity = log(n) i.e. total number of bits
        while (t != 0) {
            if ((t & 1) == 1)
                res++;

            t = t >> 1;
        }*/

        // Time complexity = number of set bits ⬇️
        // 💡 Finding number of set bits
        while (t != 0) {
            t = t & (t - 1); // clears the least significant set bit
            res++;
        }
        return res;
    }
```

## XOR Problems

### Find the element that appears once in an array where every other element appears twice

`Time Complexity: O(n)`<br>
`Space Complexity: O(1)`
```cpp

int singleNumber(vector<int> arr) {
        int res = 0;

        for (int a : arr) {
            res ^= a;
        }
        return res;
    }

```

### Find the two non-repeating elements in an array of repeating elements

`Time Complexity: O(n)`<br>
`Space Complexity: O(1)`
```cpp
vector<int> twoUniqueNumbers(vector<int> arr) {
        int temp = 0;

        for (int a : arr)
            temp ^= a;

        temp = temp & -temp; // sets rightmost set bit of temp (let's say ith bit)
        // at this bit both a and b will have distinct bits
        // we will separate array in two parts
        // 1 -> ith bit is set
        // 2 -> ith bit is clear

        int a = 0;
        int b = 0;

        for (int x : arr) {
            // ith bit is clear
            if ((temp & x) == 0)
                a ^= x; // duplicates will be cancelled out to 0
            // ith bit is set
            else
                b ^= x; // duplicates will be cancelled out to 0
        }
        vector<int> ans;
        ans.push_back(a);
        ans.push_back(b);
        return ans
    }
```

### Unique element in an array where all elements occur thrice except one

`Time Complexity: O(n)`<br>
`Space Complexity: O(1)`
> This is java code, i will update this with cpp code later
```java
// can be generelised for k occurances
static int singleNumber(int[] arr) {
        int[] bitCount = new int[32]; // 32-bit integer

        // for each bit
        for (int i = 0; i < bitCount.length; i++) {
            // for each number
            for (int k : arr) {
                if ((k & (1 << i)) != 0) // ith  bit
                    bitCount[i]++;
            }
        }

        int res = 0;
        // traversing bit count array
        for (int i = 0; i < bitCount.length; i++) {
            bitCount[i] = bitCount[i] / 3 == 0 ? 0 : bitCount[i] % 3; // set bits which are not multiple of 3 (unique)
            res += Math.pow(2, i) * bitCount[i]; // compute unique number along with
        }
        return res;
    }
```

<!-- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  -->

<hr>

# Dynamic Programming (DP)

> Overlapping Problems :- Whenever we tend to solve same problem again and again, it is called overlapping sub problems.

> Memoization :- We tend to store the value of sub problems in some map/table, so that we will not have to solve it again.

## 1-D Problems

### Understanding if it is a DP problem
> if questions are like
  - count the total number of ways.
  - Multiple ways to do, but find out min/max output.
> try all possible ways (count, best possible way)

in these type of case we tend to apply recursion

### How to approach a problem
- Try to represnt the problem in terms of index.
- Figure out base case.
- Do all possible stuffs on that index, according to the problem statement.
- Return whatever is required.
  - Sum of all stuffs - count all ways.
  - min/max (of all stuffs).

### Memoization
> Top-down - Go from required answer to base case
- uses recursion
- required space complexity is more because of stack space used

### Tabulation
> Bottom-up - Move from base case to required answer
- iteration is used
- more efficient in term of space complexity
- space complexity can further be optimised

 
<hr>

`Variation of fibonacci series`

## [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

<div class="content__u3I1 question-content__JfgR"><div><p>You are climbing a staircase. It takes <code>n</code> steps to reach the top.</p>

<p>Each time you can either climb <code>1</code> or <code>2</code> steps. In how many distinct ways can you climb to the top?</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> n = 2
<strong>Output:</strong> 2
<strong>Explanation:</strong> There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> n = 3
<strong>Output:</strong> 3
<strong>Explanation:</strong> There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 45</code></li>
</ul>
</div></div>

`Simple DP` `Top-down`

```cpp
class Solution {
private:
    int helperClimbStairs(int n,vector<int> &dp){
        if(n==0) return 1;
        if(dp[n]!=-1) return dp[n];
        int oneStep=helperClimbStairs(n-1,dp);
        int twoStep=0;
        if(n>1) twoStep=helperClimbStairs(n-2,dp);
        return dp[n]=oneStep+twoStep;
    }
public:
    int climbStairs(int n) {
        vector<int> dp(n+1,-1);
        return helperClimbStairs(n,dp);
    }
};
```

`DP Tabulation` `Bottom-up`

```cpp
class Solution {
public:
    int climbStairs(int n) {
        vector<int> dp(n+1,0);
        dp[0]=1;
        for(int i=1;i<=n;i++){
            dp[i]=dp[i-1];
            if(i>1) dp[i]+=dp[i-2];
        }
        return dp[n];
    }
};
```

> Space can be further optimised, since we are using only previous and second previous elements for calculating current elements.

```cpp
class Solution {
public:
    int climbStairs(int n) {
        int prev=0,secondPrev=0,current=0;
        prev=1;
        for(int i=1;i<=n;i++){
            current=prev;
            if(i>1) current+=secondPrev;
            secondPrev=prev;
            prev=current;
        }
        return prev;
    }
};
```


<hr>

## [Frog Jump](https://www.codingninjas.com/codestudio/problems/frog-jump_3621012)

<div _ngcontent-serverapp-c177="" class="problem-description-container"><div _ngcontent-serverapp-c177="" class="problem-statement-title-container"><div _ngcontent-serverapp-c177="" class="problem-statement-title">Problem Statement</div><div _ngcontent-serverapp-c177="" class="suggest-edit ng-star-inserted"> Suggest Edit </div><!----><!----><!----></div><div>There is a frog on the 1st step of an N stairs long staircase. The frog wants to reach the Nth stair. HEIGHT[i] is the height of the (i+1)th stair.If Frog jumps from ith to jth stair, the energy lost in the jump is given by |HEIGHT[i-1] - HEIGHT[j-1] |.In the Frog is on ith staircase, he can jump either to (i+1)th stair or to (i+2)th stair. Your task is to find the minimum total energy used by the frog to reach from 1st stair to Nth stair.</h4>


<h5 id="for-example">For Example</h5>

<pre><code>If the given ‘HEIGHT’ array is [10,20,30,10], the answer 20 as the frog can jump from 1st stair to 2nd stair (|20-10| = 10 energy lost) and then a jump from 2nd stair to last stair (|10-20| = 10 energy lost). So, the total energy lost is 20.
</code></pre>

<h5 id="input-format">Input Format:</h5>

<pre><code>The first line of the input contains an integer, 'T,’ denoting the number of test cases.

The first line of each test case contains a single integer,' N’, denoting the number of stairs in the staircase,

The next line contains ‘HEIGHT’ array.
</code></pre>

<h5 id="output-format">Output Format:</h5>

<pre><code>For each test case, return an integer corresponding to the minimum energy lost to reach the last stair.
</code></pre>

<h5 id="note">Note:</h5>

<pre><code>You do not need to print anything. It has already been taken care of. Just implement the given function.
</code></pre>

<h5 id="constraints">Constraints:</h5>

<pre><code>1 &lt;= T &lt;= 10
1 &lt;= N &lt;= 100000.
1 &lt;= HEIGHTS[i] &lt;= 1000 .

Time limit: 1 sec
</code></pre>
</div><div _ngcontent-serverapp-c177="" class="description ng-star-inserted"><h5>Sample Input 1:</h5>

<pre><code>2
4

10 20 30 10
3
10 50 10
</code></pre>

<h5>Sample Output 1:</h5>

<pre><code>20
0
</code></pre>

<h5>Explanation of sample input 1:</h5>

<pre><code>For the first test case,
The frog can jump from 1st stair to 2nd stair (|20-10| = 10 energy lost).
Then a jump from the 2nd stair to the last stair (|10-20| = 10 energy lost).
So, the total energy lost is 20 which is the minimum. 
Hence, the answer is 20.

For the second test case:
The frog can jump from 1st stair to 3rd stair (|10-10| = 0 energy lost).
So, the total energy lost is 0 which is the minimum. 
Hence, the answer is 0.
</code></pre>

<h5>Sample Input 2:</h5>

<pre><code>2
8
7 4 4 2 6 6 3 4 
6
4 8 3 10 4 4 
</code></pre>

<h5>Sample Output 2:</h5>

<pre><code>7
2
</code></pre>
</div><!----><!----><!----></div>

```cpp

int helper(int i,vector<int> &heights,vector<int> &dp){
    if(i==heights.size()-1) return 0;
    if(dp[i]!=-1) return dp[i];
    int one=abs(heights[i]-heights[i+1]) + helper(i+1,heights,dp);
    int two=INT_MAX;
    if(i<heights.size()-2) two=abs(heights[i]-heights[i+2]) + helper(i+2,heights,dp);
    return dp[i]=min(one,two);
}
int frogJump(int n, vector<int> &heights){
    vector<int> dp(n+1,-1);
    return helper(0,heights,dp);
}

```
> In above solution i have moved form 0th index to last index

> We can also move from last index to 0th index

```cpp
int helper(int i,vector<int> &heights,vector<int> &dp){
    if(i==0) return 0;
    if(dp[i]!=-1) return dp[i];
    int one=abs(heights[i]-heights[i-1]) + helper(i-1,heights,dp);
    int two=INT_MAX;
    if(i>1) two=abs(heights[i]-heights[i-2]) + helper(i-2,heights,dp);
    return dp[i]=min(one,two);
}
int frogJump(int n, vector<int> &heights){
    vector<int> dp(n+1,-1);
    return helper(heights.size()-1,heights,dp);
}
```

```Tabulation form```

```cpp

int frogJump(int n, vector<int> &heights){
    vector<int> dp(n,0);
    for(int i=1;i<n;i++){
        int one=abs(heights[i]-heights[i-1])+dp[i-1];
        int two=INT_MAX;
        if(i>1) two=abs(heights[i]-heights[i-2]) + dp[i-2];
        dp[i]=min(one,two);
    }
    return dp[n-1];
}

```
> Space can further be optimised, since we are using only `dp[i-1]` and `dp[i-2]`.

```cpp
int frogJump(int n, vector<int> &heights){
   int prev=0,secondPrv=0,current=0;
    for(int i=1;i<n;i++){
        int one=abs(heights[i]-heights[i-1])+prev;
        int two=INT_MAX;
        if(i>1) two=abs(heights[i]-heights[i-2]) + secondPrv;
        current=min(one,two);
        secondPrv=prev;
        prev=current;
    }
    return prev;
}
```


<hr>

## [198. House Robber](https://leetcode.com/problems/house-robber/)

<div class="content__u3I1 question-content__JfgR"><div><p>You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and <b>it will automatically contact the police if two adjacent houses were broken into on the same night</b>.</p>



<p>Given an integer array <code>nums</code> representing the amount of money of each house, return <em>the maximum amount of money you can rob tonight <b>without alerting the police</b></em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,3,1]
<strong>Output:</strong> 4
<strong>Explanation:</strong> Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [2,7,9,3,1]
<strong>Output:</strong> 12
<strong>Explanation:</strong> Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 100</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 400</code></li>
</ul>
</div></div>

```cpp
class Solution {
private:
    int helperRob(int index,vector<int>& nums,vector<int>& dp){
        if(index==0) return nums[0];
        if(index<0) return 0;
        if(dp[index]!=-1) return dp[index];
        int pick = nums[index] + helperRob(index-2,nums,dp);
        int notPick = helperRob(index-1,nums,dp);
        return dp[index]=max(pick,notPick);
    }
public:
    int rob(vector<int>& nums) {
        vector<int> dp(nums.size(),-1);
        return helperRob(nums.size()-1,nums,dp);
    }
};
```

> Tabulation

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {    
        vector<int> dp(nums.size(),-1);
        dp[0]=nums[0];
        for(int i=1;i<nums.size();i++){
            int pick=nums[i]+ (i>1?dp[i-2]:0);
            int notPick=dp[i-1];
            dp[i]=max(pick,notPick);
        }
        return dp[nums.size()-1];
    }
};
```
> Space optimised tabulation

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int prev=nums[0],prev2=0;
        vector<int> dp(nums.size(),-1);
        dp[0]=nums[0];
        for(int i=1;i<nums.size();i++){
            int pick=nums[i]+ prev2;
            int notPick=prev;
            int current=max(pick,notPick);
            prev2=prev;
            prev=current;
        }
        return prev;
    }
};
```

<hr>

## [213. House Robber II](https://leetcode.com/problems/house-robber-ii/)

> [Follow up for House Robber 1](https://leetcode.com/problems/house-robber/)
<div class="content__u3I1 question-content__JfgR"><div><p>You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are <strong>arranged in a circle.</strong> That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and&nbsp;<b>it will automatically contact the police if two adjacent houses were broken into on the same night</b>.</p>



<p>Given an integer array <code>nums</code> representing the amount of money of each house, return <em>the maximum amount of money you can rob tonight <strong>without alerting the police</strong></em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [2,3,2]
<strong>Output:</strong> 3
<strong>Explanation:</strong> You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,3,1]
<strong>Output:</strong> 4
<strong>Explanation:</strong> Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,3]
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 100</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 1000</code></li>
</ul>
</div></div>

```cpp
class Solution {
private:
    int helperRob(bool f,vector<int>& nums){
        int i=(f?2:1);
        int prev=nums[i-1],prev2=0;
        for(;i<nums.size();i++){
            int pick=nums[i]+prev2;
            int notPick=prev;
            int current=max(pick,notPick);
            prev2=prev;
            prev=current;
        }
        return prev;
    }
public:
    int rob(vector<int>& nums) {
        if(nums.size()==1) return nums[0];
        int front=nums[0],back=nums[nums.size()-1];
        nums.pop_back();
        int withFront=helperRob(false,nums);
        nums.push_back(back);
        int withBack=helperRob(true,nums);
        return max(withFront,withBack);
    }
};
```
> Calling the same iterative function (Optimised solution of House Robber) with either including first element or last element (not includin both of them) because in cyclic fashion, first and last element will always be adjacent to each other, so he cannot rob both houses.


<hr>

## [Ninja’s Training](https://www.codingninjas.com/codestudio/problems/ninja-s-training_3621003)

<div _ngcontent-serverapp-c177="" class="problem-description-container"><div _ngcontent-serverapp-c177="" class="problem-statement-title-container"><div _ngcontent-serverapp-c177="" class="problem-statement-title">Problem Statement</div><div _ngcontent-serverapp-c177="" class="suggest-edit ng-star-inserted"> Suggest Edit </div><!----><!----><!----></div><div><h4 >Ninja is planing this ‘N’ days-long training schedule. Each day, he can perform any one of these three activities. (Running, Fighting Practice or Learning New Moves). Each activity has some merit points on each day. As Ninja has to improve all his skills, he can’t do the same activity in two consecutive days. Can you help Ninja find out the maximum merit points Ninja can earn?</h4>



<h4>You are given a 2D array of size N*3  ‘POINTS’ with the points corresponding to each day and activity. Your task is to calculate the maximum number of merit points that Ninja can earn.</h4>


<h5 id="for-example">For Example</h5>

<pre><code>If the given ‘POINTS’ array is [[1,2,5], [3 ,1 ,1] ,[3,3,3] ],the answer will be 11 as 5 + 3 + 3.
</code></pre>

<h5 id="input-format">Input Format:</h5>

<pre><code>The first line of the input contains an integer, 'T,’ denoting the number of test cases.

The first line of each test case contains a single integer,' N’, denoting the number of days.

The next ‘N’ lines of each test case have 3 integers corresponding to POINTS[i].
</code></pre>

<h5 id="output-format">Output Format:</h5>

<pre><code>For each test case, return an integer corresponding to the maximum coins  Ninja can collect.
</code></pre>

<h5 id="note">Note:</h5>

<pre><code>You do not need to print anything. It has already been taken care of. Just implement the given function.
</code></pre>

<h5 id="constraints">Constraints:</h5>

<pre><code>1 &lt;= T &lt;= 10
1 &lt;= N &lt;= 100000.
1 &lt;= values of POINTS arrays &lt;= 100 .

Time limit: 1 sec
</code></pre>
</div><div _ngcontent-serverapp-c177="" class="description ng-star-inserted"><h5>Sample Input 1:</h5>

<pre><code>2
3
1 2 5 
3 1 1
3 3 3
3
10 40 70
20 50 80
30 60 90
</code></pre>

<h5>Sample Output 1:</h5>

<pre><code>11
210
</code></pre>

<h5>Explanation of sample input 1:</h5>

<pre><code>For the first test case,
One of the answers can be:
On the first day, Ninja will learn new moves and earn 5 merit points. 
On the second day, Ninja will do running and earn 3 merit points. 
On the third day, Ninja will do fighting and earn 3 merit points. 
The total merit point is 11 which is the maximum. 
Hence, the answer is 11.

For the second test case:
One of the answers can be:
On the first day, Ninja will learn new moves and earn 70 merit points. 
On the second day, Ninja will do fighting and earn 50 merit points. 
On the third day, Ninja will learn new moves and earn 90 merit points. 
The total merit point is 210 which is the maximum. 
Hence, the answer is 210.
</code></pre>

<h5>Sample Input 2:</h5>

<pre><code>2
3
18 11 19
4 13 7
1 8 13
2
10 50 1
5 100 11
</code></pre>

<h5>Sample Output 2:</h5>

<pre><code>45
110
</code></pre>
</div><!----><!----><!----></div>


```cpp
#include <bits/stdc++.h>
int helper(int day,int last,vector<vector<int>> &points,vector<vector<int>> &dp){
    if(day==0){
        int maxi=INT_MIN;
        for(int i=0;i<3;i++) if(i!=last) maxi=max(maxi,points[0][i]);
        return maxi;
    }
    if(last!=3&&dp[day][last]!=-1) return dp[day][last];
    int maxi=INT_MIN;
    for(int i=0;i<3;i++)
        if(i!=last)
            maxi=max(maxi,points[day][i]+helper(day-1,i,points,dp));
    return dp[day][last]=maxi;
}

int ninjaTraining(int n, vector<vector<int>> &points){
    vector<vector<int>> dp(n,vector<int>(3,-1));
    return helper(n-1,3,points,dp);
}
```

> Tabulation

```cpp
int ninjaTraining(int n, vector<vector<int>> &points){
    vector<vector<int>> dp(n,vector<int>(4,-1));
    dp[0][0]=max(points[0][1],points[0][2]);
    dp[0][1]=max(points[0][0],points[0][2]);
    dp[0][2]=max(points[0][0],points[0][1]);
    dp[0][3]=max(points[0][0],dp[0][0]);
    // dp[0][3]=max(points[0][0],max(points[0][1],points[0][2]));
    for(int i=1;i<n;i++){
        for(int j=0;j<4;j++){
            int maxi=INT_MIN;
           for(int k=0;k<3;k++){
               if(j!=k)
                   maxi=max(maxi,points[i][k]+dp[i-1][k]);
            dp[i][j]=maxi;
           }
        }
    }
    return dp[n-1][3];
}
```

> Space optimised tabulation

```cpp
int ninjaTraining(int n, vector<vector<int>> &points){
    vector<int> prev(4,0),curr(4,0);
    prev[0]=max(points[0][1],points[0][2]);
    prev[1]=max(points[0][0],points[0][2]);
    prev[2]=max(points[0][0],points[0][1]);
    prev[3]=max(points[0][0],prev[0]);
    // dp[0][3]=max(points[0][0],max(points[0][1],points[0][2]));
    for(int i=1;i<n;i++){
        for(int j=0;j<4;j++){
            int maxi=INT_MIN;
           for(int k=0;k<3;k++){
               if(j!=k)
                   maxi=max(maxi,points[i][k]+prev[k]);
            curr[j]=maxi;
           }
        }
        prev=curr;
    }
    return prev[3];
}
```


<hr>

## [62. Unique Paths](https://leetcode.com/problems/unique-paths/)

<div class="content__u3I1 question-content__JfgR"><div><p>There is a robot on an <code>m x n</code> grid. The robot is initially located at the <strong>top-left corner</strong> (i.e., <code>grid[0][0]</code>). The robot tries to move to the <strong>bottom-right corner</strong> (i.e., <code>grid[m - 1][n - 1]</code>). The robot can only move either down or right at any point in time.</p>

<p>Given the two integers <code>m</code> and <code>n</code>, return <em>the number of possible unique paths that the robot can take to reach the bottom-right corner</em>.</p>

<p>The test cases are generated so that the answer will be less than or equal to <code>2 * 10<sup>9</sup></code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img src="https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png" style="width: 400px; height: 183px;">
<pre><strong>Input:</strong> m = 3, n = 7
<strong>Output:</strong> 28
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> m = 3, n = 2
<strong>Output:</strong> 3
<strong>Explanation:</strong> From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -&gt; Down -&gt; Down
2. Down -&gt; Down -&gt; Right
3. Down -&gt; Right -&gt; Down
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= m, n &lt;= 100</code></li>
</ul>
</div></div>

```cpp
class Solution {
private:
    int helper(int i,int j,vector<vector<int>> &dp){
        if(i==0&&j==0){
            return 1;            
        }
        if(dp[i][j]!=-1) return dp[i][j];
        int right=0,down=0;
        if(j>0) right=helper(i,j-1,dp);
        if(i>0) down=helper(i-1,j,dp);
        return dp[i][j]=right+down;
    }
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m,vector<int> (n,-1));
        return helper(m-1,n-1,dp);
    }
};
```

> Tabulation

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m,vector<int> (n,-1));
        dp[0][0]=1;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                int right=0,down=0;
                if(j>0) right=dp[i][j-1];
                if(i>0) down=dp[i-1][j];
                if(i==0&&j==0) continue;
                dp[i][j]=right+down;
            }
        }
        return dp[m-1][n-1];
    }
};

```

> Space optimised tabulation

```cpp
class Solution {
public:
    // DP- TABULATION FORM -SPACE OPTIMISED
    int uniquePaths(int m,int n){
        vector<int> up(n,1),current(n,1);
        for(int i=1;i<m;i++){
            for(int j=0;j<n;j++){
                if(j==0) current[j]=1;
                else current[j]=current[j-1]+up[j];
            }
            up=current;
        }
        return up[n-1];
    }
};
```

<hr>

## [63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)

<div class="content__u3I1 question-content__JfgR"><div><p>You are given an <code>m x n</code> integer array <code>grid</code>. There is a robot initially located at the <b>top-left corner</b> (i.e., <code>grid[0][0]</code>). The robot tries to move to the <strong>bottom-right corner</strong> (i.e., <code>grid[m-1][n-1]</code>). The robot can only move either down or right at any point in time.</p>

<p>An obstacle and space are marked as <code>1</code> or <code>0</code> respectively in <code>grid</code>. A path that the robot takes cannot include <strong>any</strong> square that is an obstacle.</p>

<p>Return <em>the number of possible unique paths that the robot can take to reach the bottom-right corner</em>.</p>

<p>The testcases are generated so that the answer will be less than or equal to <code>2 * 10<sup>9</sup></code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg" style="width: 242px; height: 242px;">
<pre><strong>Input:</strong> obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
<strong>Output:</strong> 2
<strong>Explanation:</strong> There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -&gt; Right -&gt; Down -&gt; Down
2. Down -&gt; Down -&gt; Right -&gt; Right
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg" style="width: 162px; height: 162px;">
<pre><strong>Input:</strong> obstacleGrid = [[0,1],[0,0]]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == obstacleGrid.length</code></li>
	<li><code>n == obstacleGrid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 100</code></li>
	<li><code>obstacleGrid[i][j]</code> is <code>0</code> or <code>1</code>.</li>
</ul>
</div></div>

```cpp
class Solution {
private:
    int helper(int i,int j,vector<vector<int>>& obstacleGrid,vector<vector<int>> &dp){
        if(obstacleGrid[i][j]) return 0;
        if(i==0&&j==0) return 1;
        if(dp[i][j]!=-1) return dp[i][j];
        int right=0,down=0;
        if(i>0) down=helper(i-1,j,obstacleGrid,dp);
        if(j>0) right=helper(i,j-1,obstacleGrid,dp);
        return dp[i][j]=right+down;
    }
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        vector<vector<int>> dp(obstacleGrid.size(),vector<int> (obstacleGrid[0].size(),-1));
        dp[0][0]=1;
        return helper(obstacleGrid.size()-1,obstacleGrid[0].size()-1,obstacleGrid,dp);
    }
};

```

> Tabulation

```cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        vector<vector<int>> dp(obstacleGrid.size(),vector<int> (obstacleGrid[0].size(),0));
        if(!obstacleGrid[0][0]) dp[0][0]=1;
        for(int i=0;i<obstacleGrid.size();i++){
            for(int j=0;j<obstacleGrid[0].size();j++){
                if(i==0&&j==0) continue;
                if(obstacleGrid[i][j]) continue;
                int right=0,down=0;
                if(i>0) down=dp[i-1][j];
                if(j>0) right=dp[i][j-1];
                dp[i][j]=right+down;                
            }
        }
        
        return dp[obstacleGrid.size()-1][obstacleGrid[0].size()-1];
    }
};
```

<hr>

## [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)

<div class="content__u3I1 question-content__JfgR"><div><p>Given a <code>m x n</code> <code>grid</code> filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.</p>


<p><strong>Note:</strong> You can only move either down or right at any point in time.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg" style="width: 242px; height: 242px;">
<pre><strong>Input:</strong> grid = [[1,3,1],[1,5,1],[4,2,1]]
<strong>Output:</strong> 7
<strong>Explanation:</strong> Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> grid = [[1,2,3],[4,5,6]]
<strong>Output:</strong> 12
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 200</code></li>
	<li><code>0 &lt;= grid[i][j] &lt;= 100</code></li>
</ul>
</div></div>

```cpp
class Solution{
private:
    int helper(int i,int j,vector<vector<int>> &grid,vector<vector<int>> &dp){
        if(i==grid.size()-1&&j==grid[0].size()-1) return grid[i][j];
        if(dp[i][j]!=-1) return dp[i][j];
        int right=INT_MAX,down=INT_MAX;
        if(j<grid[0].size()-1) right=helper(i,j+1,grid,dp);
        if(i<grid.size()-1) down=helper(i+1,j,grid,dp);
        return dp[i][j]=min(right,down)+grid[i][j];
    }
public:
    int minPathSum(vector<vector<int>> &grid){
        vector<vector<int>> dp(grid.size(),vector<int> (grid[0].size(),-1));
        return helper(0,0,grid,dp);
    }
};
```
> Tabulation

```cpp
class Solution{
public:
    int minPathSum(vector<vector<int>> &grid){
        vector<vector<int>> dp(grid.size(),vector<int>(grid[0].size(),-1));
        dp[0][0]=grid[0][0];
        for(int i=0;i<grid.size();i++){
            for(int j=0;j<grid[0].size();j++){
                if(i==0&&j==0) continue;
                int right=INT_MAX,down=INT_MAX;
                if(j>0) right=dp[i][j-1];
                if(i>0) down=dp[i-1][j];
                dp[i][j]=min(right,down)+grid[i][j];
            }
        }
        return dp[grid.size()-1][grid[0].size()-1];
    }
};
```

> Space optimised tabulation

```cpp
class Solution{
public:
    int minPathSum(vector<vector<int>> &grid){
        vector<int> temp(grid[0].size(),0),current(grid[0].size(),0);
        current[0]=grid[0][0];
        for(int i=0;i<grid.size();i++){
            for(int j=0;j<grid[0].size();j++){
                if(i==0&&j==0) continue;
                int left=INT_MAX,up=INT_MAX;
                if(j>0) left=current[j-1];
                if(i>0) up=temp[j];
                current[j]=min(left,up)+grid[i][j];
            }
            temp=current;
        }
        return temp[grid[0].size()-1];
    }
};
```


<hr>

## [120. Triangle](https://leetcode.com/problems/triangle/)

<div class="content__u3I1 question-content__JfgR"><div><p>Given a <code>triangle</code> array, return <em>the minimum path sum from top to bottom</em>.</p>

<p>For each step, you may move to an adjacent number of the row below. More formally, if you are on index <code>i</code> on the current row, you may move to either index <code>i</code> or index <code>i + 1</code> on the next row.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
<strong>Output:</strong> 11
<strong>Explanation:</strong> The triangle looks like:
   <u>2</u>
  <u>3</u> 4
 6 <u>5</u> 7
4 <u>1</u> 8 3
The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> triangle = [[-10]]
<strong>Output:</strong> -10
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= triangle.length &lt;= 200</code></li>
	<li><code>triangle[0].length == 1</code></li>
	<li><code>triangle[i].length == triangle[i - 1].length + 1</code></li>
	<li><code>-10<sup>4</sup> &lt;= triangle[i][j] &lt;= 10<sup>4</sup></code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you&nbsp;do this using only <code>O(n)</code> extra space, where <code>n</code> is the total number of rows in the triangle?</div></div>

```cpp
class Solution {
private:
    int helper(int i,int j,vector<vector<int>>& triangle,vector<vector<int>> &dp){
        if(i>=triangle.size()-1) return triangle[i][j];
        if(dp[i][j]!=-1) return dp[i][j];
        int minus=0,plus=0;
        if(j<triangle[i+1].size()-1) plus=helper(i+1,j+1,triangle,dp);
        minus=helper(i+1,j,triangle,dp);
        return dp[i][j]=min(plus,minus)+triangle[i][j];
    }
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        vector<vector<int>> dp;
        for(int i=0;i<triangle.size();i++){
            vector<int> temp(i+1,-1);
            dp.push_back(temp);
        }
        return helper(0,0,triangle,dp);
    }
};
```
> Tabulation

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n=triangle.size();
        vector<vector<int>> dp;
        for(int i=0;i<n;i++){
            vector<int> temp(i+1,-1);
            dp.push_back(temp);
        }
        for(int i=0;i<n;i++) dp[n-1][i]=triangle[n-1][i];
        for(int i=n-2;i>=0;i--)
            for(int j=i;j>=0;j--) dp[i][j]=min(dp[i+1][j],dp[i+1][j+1])+triangle[i][j];
        return dp[0][0];
    }
};
```

> Space optimised tabulation

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n=triangle.size();
        vector<int> prev(n,0);
        for(int i=0;i<n;i++) prev[i]=triangle[n-1][i];
        for(int i=n-2;i>=0;i--){
            vector<int> curr(i+1,0);
            for(int j=i;j>=0;j--) curr[j]=min(prev[j],prev[j+1])+triangle[i][j];
            prev=curr;
        }
        return prev[0];
    }
};
```


<hr>

## [931. Minimum Falling Path Sum](https://leetcode.com/problems/minimum-falling-path-sum/)

<div class="content__u3I1 question-content__JfgR"><div><p>Given an <code>n x n</code> array of integers <code>matrix</code>, return <em>the <strong>minimum sum</strong> of any <strong>falling path</strong> through</em> <code>matrix</code>.</p>

<p>A <strong>falling path</strong> starts at any element in the first row and chooses the element in the next row that is either directly below or diagonally left/right. Specifically, the next element from position <code>(row, col)</code> will be <code>(row + 1, col - 1)</code>, <code>(row + 1, col)</code>, or <code>(row + 1, col + 1)</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/11/03/failing1-grid.jpg" style="width: 499px; height: 500px;">
<pre><strong>Input:</strong> matrix = [[2,1,3],[6,5,4],[7,8,9]]
<strong>Output:</strong> 13
<strong>Explanation:</strong> There are two falling paths with a minimum sum as shown.
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/11/03/failing2-grid.jpg" style="width: 164px; height: 365px;">
<pre><strong>Input:</strong> matrix = [[-19,57],[-40,-5]]
<strong>Output:</strong> -59
<strong>Explanation:</strong> The falling path with a minimum sum is shown.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == matrix.length == matrix[i].length</code></li>
	<li><code>1 &lt;= n &lt;= 100</code></li>
	<li><code>-100 &lt;= matrix[i][j] &lt;= 100</code></li>
</ul>
</div></div>

```cpp
class Solution {
private:
    int helper(int i,int j,vector<vector<int>>& matrix,vector<vector<int>>& dp){
        if(i==0) return matrix[i][j];
        if(dp[i][j]!=-1) return dp[i][j];
        int d=matrix[i][j]+helper(i-1,j,matrix,dp);
        int dl=matrix[i][j],dr=matrix[i][j];
        if(j>0) dl+=helper(i-1,j-1,matrix,dp);
        else dl+=1e9;
        if(j+1<matrix[0].size()) dr+=helper(i-1,j+1,matrix,dp);
        else dr+=1e9;
        return dp[i][j]=min(d,min(dl,dr));
    }
public:
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int mini=INT_MAX;
        vector<vector<int>> dp(matrix.size(),vector<int>(matrix[0].size(),-1));
        for(int i=0;i<matrix[0].size();i++)
            mini=min(mini,helper(matrix.size()-1,i,matrix,dp));
        return mini;
    }
};
```
> Tabulation

```cpp
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int mini=INT_MAX,n=matrix.size();
        vector<vector<int>> dp(n,vector<int>(n,-1));
        for(int i=0;i<n;i++) dp[0][i]=matrix[0][i];
        for(int i=1;i<n;i++){
            for(int j=0;j<n;j++){
                int d=matrix[i][j]+dp[i-1][j];
                int dl=matrix[i][j],dr=matrix[i][j];
                if(j>0) dl+=dp[i-1][j-1];
                else dl+=1e9;
                if(j+1<matrix[0].size()) dr+=dp[i-1][j+1];
                else dr+=1e9; 
                dp[i][j]=min(d,min(dr,dl));
            }
        }
        for(int i=0;i<n;i++) mini=min(mini,dp[n-1][i]);
        return mini;
    }
};
```

> Space optimised tabulation

```cpp
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int mini=INT_MAX,n=matrix.size();
        vector<int> prev(n,-1);
        for(int i=0;i<n;i++) prev[i]=matrix[0][i];
        for(int i=1;i<n;i++){
            vector<int> curr(n,-1);
            for(int j=0;j<n;j++){
                int d=matrix[i][j]+prev[j];
                int dl=matrix[i][j],dr=matrix[i][j];
                if(j>0) dl+=prev[j-1];
                else dl+=1e9;
                if(j+1<matrix[0].size()) dr+=prev[j+1];
                else dr+=1e9; 
                curr[j]=min(d,min(dr,dl));
            }
            prev=curr;
        }
        for(int i=0;i<n;i++) mini=min(mini,prev[i]);
        return mini;
    }
};
```


<hr>

## [494. Target Sum](https://leetcode.com/problems/target-sum/)

<div class="content__u3I1 question-content__JfgR"><div><p>You are given an integer array <code>nums</code> and an integer <code>target</code>.</p>


<p>You want to build an <strong>expression</strong> out of nums by adding one of the symbols <code>'+'</code> and <code>'-'</code> before each integer in nums and then concatenate all the integers.</p>

<ul>
	<li>For example, if <code>nums = [2, 1]</code>, you can add a <code>'+'</code> before <code>2</code> and a <code>'-'</code> before <code>1</code> and concatenate them to build the expression <code>"+2-1"</code>.</li>
</ul>

<p>Return the number of different <strong>expressions</strong> that you can build, which evaluates to <code>target</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,1,1,1,1], target = 3
<strong>Output:</strong> 5
<strong>Explanation:</strong> There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1], target = 1
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 20</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 1000</code></li>
	<li><code>0 &lt;= sum(nums[i]) &lt;= 1000</code></li>
	<li><code>-1000 &lt;= target &lt;= 1000</code></li>
</ul>
</div></div>

```cpp
class Solution {
private:
    int helper(int index,int target,
               vector<int>& nums,
               vector<unordered_map<int,int>>& dp){
        if(index==0){
            if(target+nums[0]==0&&target-nums[0]==0) return 2;
            else if(target+nums[0]==0||target-nums[0]==0) return 1;
            else return 0;
        }
        if(dp[index].find(target)!=dp[index].end()) return dp[index][target];
        int one=helper(index-1,target-nums[index],nums,dp);
        int two=helper(index-1,target+nums[index],nums,dp);
        return dp[index][target]=one+two;
    }
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        vector<unordered_map<int,int>> dp(nums.size());
        return helper(nums.size()-1,target,nums,dp);
    }
};
```
> This cannot be further optimised, beacuse we can have negative values of target.


<hr>

## [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

> This is another variant of target sum

<div class="content__u3I1 question-content__JfgR"><div><p>Given a <strong>non-empty</strong> array <code>nums</code> containing <strong>only positive integers</strong>, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,5,11,5]
<strong>Output:</strong> true
<strong>Explanation:</strong> The array can be partitioned as [1, 5, 5] and [11].
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,3,5]
<strong>Output:</strong> false
<strong>Explanation:</strong> The array cannot be partitioned into equal sum subsets.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 200</code></li>
	<li><code>1 &lt;= nums[i] &lt;= 100</code></li>
</ul>
</div></div>

```cpp
class Solution {
private:
        bool helper(int index,int target,vector<int>& nums,
                    vector<vector<int>> &dp){
        if(target==0) return true;
        if(index==nums.size()) return target==0;
        if(dp[index][target]!=-1) return dp[index][target];
        bool pick=false;
        if(target>=nums[index]) pick=helper(index+1,target-nums[index],nums,dp);
        bool notPick=helper(index+1,target,nums,dp);
        return dp[index][target]=pick||notPick;
    }
public:
    bool canPartition(vector<int>& nums) {
        int total=0;
        for(auto num:nums) total+=num;
        if(total&1) return false;
        int target=total/2;
        vector<vector<int>> dp(nums.size(),vector<int> (target+1,-1));
        return helper(0,target,nums,dp);
    }
};
```
> Tabulation

> Since here only positive number is used, this can be optimised to tabulation form
```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int total=0;
        for(auto num:nums) total+=num;
        if(total&1) return false;
        int target=total/2;
        vector<vector<bool>> dp(nums.size(),vector<bool> (target+1,false));
        for(int i=1;i<nums.size();i++) dp[i][0]=true;
        if(nums[0]<=target) dp[0][nums[0]]=true;
        for(int i=1;i<nums.size();i++){
            for(int j=1;j<=target;j++){
                bool pick=false;
                if(j>=nums[i]) pick=dp[i-1][j-nums[i]];
                bool notPick=dp[i-1][j];
                dp[i][j]=pick||notPick;
            }
        }
        return dp[nums.size()-1][target];
    }
};
```

> Further space optimisation

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int total=0;
        for(auto num:nums) total+=num;
        if(total&1) return false;
        int target=total/2;
        vector<bool> prev(target+1,false),curr(target+1,false);
        prev[0]=curr[0]=true;
        if(nums[0]<=target) prev[nums[0]]=true;
        for(int i=1;i<nums.size();i++){
            for(int j=1;j<=target;j++){
                bool pick=false;
                if(j>=nums[i]) pick=prev[j-nums[i]];
                bool notPick=prev[j];
                curr[j]=pick||notPick;
            }
            prev=curr;
        }
        return prev[target];
    }
};
```

# Object Oriented Programming (OOPS)


## WHY OOPS?


* C++ language was designed with the main intention of adding object-oriented features
to C language.

* As the size of the program increases, readability, maintainability and bug-free nature of i bug-tree nature 
programs decreases.

* This was the major problem with languages like C which relied upon functions or
procedures (hence the name procedural programming language)

* As a result, the possibility of not addressing the problem in an effective manner was high.
* Also, as data was almost neglected, data security was easily compromised.
* Using classes solves this problem by modelling program as a real world scenario

## PROCEDURE ORIENTED PROGRAMMING

* Consists of writing a set of instructions for the computer to follow
* Main focus is on functions and not on flow of data
* Functions can either use local or global data
* Data moves openly from function to function

## OBJECT ORIENTED PROGRAMMING
* Works on the concept of classes and objects
* A class is a template to create objects
* Treats data as a critical element.
* Decomposes the problem in objects and builds data and functions around the objects

## BASIC CONCEPTS IN OBJECT ORIENTED
PROGRAMMING
* Classes — Basic template for creating objects.
* Objects — Basic run time entities.
* Data Abstraction & Encapsulation — Wrapping data and functions into slngle unit.
* Inheritance — Properties of one class can be inherited into others.
* Polymorphism — ability to take more than one forms.
* Dynamic Binding — code which will execute is not known until the program runs.
* Message Passing — Object.message(Information) call format.

## BENEFITS OF OBJECT ORIENTED PROGRAMMING
* Better code reusability using objects and Inheritance.
* Principle of data hiding helps build secure systems.
* Multiple objects can co-exist without any interference.
* Software complexity can be easily managed.

