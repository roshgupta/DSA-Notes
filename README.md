- [Recursion](https://github.com/roshgupta/DSA-Notes#recursion)
  - [Print all Sub-Sequences](https://github.com/roshgupta/DSA-Notes#print-all-sub-sequences)
  - [Print all Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#print-all-sub-sequences-with-sum-equals-to-k)
  - [Print ONE Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#print-one-sub-sequences-with-sum-equals-to-k)
  - [Count number of Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#count-number-of-sub-sequences-with-sum-equals-to-k)
  


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
