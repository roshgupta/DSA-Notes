- [Recursion](https://github.com/roshgupta/DSA-Notes#recursion)
  - [Print all Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#print-all-sub-sequences-with-sum-equals-to-k)
  - [Print ONE Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#print-one-sub-sequences-with-sum-equals-to-k)
  - [Count number of Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#count-number-of-sub-sequences-with-sum-equals-to-k)
  


<hr>

# Recursion

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
