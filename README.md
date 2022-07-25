- [Recursion](https://github.com/roshgupta/DSA-Notes#recursion)
  - [Print all Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#print-all-sub-sequences-with-sum-equals-to-k)
  - [Print ONE Sub-Sequences with sum equals to K](https://github.com/roshgupta/DSA-Notes#print-one-sub-sequences-with-sum-equals-to-k)
  


<hr>

# Recursion

## Print all Sub-Sequences with sum equals to K

```cpp


#include <bits/stdc++.h>
using namespace std;
void printS(int ind, vector<int> &ds, int s, int sum, int arr[], int n) {
  if (ind == n) {
    if (s == sum) {
      for (auto it : ds)
        cout << it << " ";
      cout << endl;
    }
    return;
  }

  ds.push_back(arr[ind]);
  s += arr[ind];
  printS(ind + 1, ds, s, sum, arr, n);
  s -= arr[ind];
  ds.pop_back();
  printS(ind + 1, ds, s, sum, arr, n);
}

int main() {
  int arr[] = {1, 2, 1};
  int n = 3;
  int sum = 2;
  vector<int> ds;
  printS(0, ds, 0, sum, arr, n);
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
bool printS(int ind, vector<int> &ds, int s, int sum, int arr[], int n) {
  if (ind == n) {
    if (s == sum) {
      for (auto it : ds)
        cout << it << " ";
      cout << endl;
      return true;
    }
    return false;
  }

  ds.push_back(arr[ind]);
  s += arr[ind];
  if (printS(ind + 1, ds, s, sum, arr, n)) return true;
  s -= arr[ind];
  ds.pop_back();
  if (printS(ind + 1, ds, s, sum, arr, n)) return true;
  return false;
}

int main() {
  int arr[] = {1, 2, 1};
  int n = 3;
  int sum = 2;
  vector<int> ds;
  printS(0, ds, 0, sum, arr, n);
  return 0;
}


```
> here, if any sub sequence is printed, we will return true.
> as soon as a true is returned, further calls will not be made, since it checks for returned value and calls next function only if the returned value is false.

