# Contents - Array
- [<span style = "font-size:25px; color:green;"> Easy </span>](#easy)
- [<span style = "font-size:25px; color:orange;"> Medium </span>](#medium)
- [<span style = "font-size:25px; color:red;"> Hard </span>](#hard)


---

#  <span id="easy" style = "color:green">Easy </span> &nbsp; [<span style = "font-size:10px;color:orange;"> Medium</span>](#medium) &nbsp; [<span style = "font-size:10px;color:red;">Hard</span>](#hard)

### <span style = "color:violet"> Question 3 -  Check if Array Is Sorted and Rotated  - </span> [Link](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated)

#### <b style="color:Aqua"> Problem Statement : </b>

Given an array nums, return true if the array was originally sorted in non-decreasing order, then rotated some number of positions (including zero). Otherwise, return false.

There may be duplicates in the original array.

<ul>
<li>Example 1:</li>
<ol type=1>
<li>Input: nums = [3,4,5,1,2] </li>
<li>Output: true </li>
<li>Explanation: [1,2,3,4,5] is the original sorted array.
    You can rotate the array by x = 3 positions to begin on the the element of value 3: [3,4,5,1,2].</li>
</ol>
</ul>

<ul>
<li>Example 2: </li>
<ol type=1>
<li>Input: nums = [2,1,3,4] </li>
<li>Output: false </li>
<li>Explanation: There is no sorted array once rotated that can make nums. </li>
</ol>
</ul>

#### <b style="color:Aqua">Logic : </b>

1. A sorted and rotated array can have atmost 1 peak (arr[i-1] < arr[i] > arr[i+1])
2. Count the number of peaks in the array.
3. Also compare the last & first element of the array.
4. If the no. of peaks <= 1 then the array is sorted & rotated. Otherwise not

#### <b style="color:Aqua">Code : </b>

```cpp 
for(int i = 1; i < n; i++) {
            if(nums[i] < nums[i-1]){
               count++; 
            } 
}
        
// Compare the last & first element as the array can be rotated
    if(nums[0] < nums[n-1]) count++;
    
```

---

### <span style = "color:violet"> Question 4 - Remove Duplicates from Sorted Array  - </span> [Link](https://leetcode.com/problems/remove-duplicates-from-sorted-array)

#### <b style="color:Aqua"> Problem Statement : </b>

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.
<ul>
    <li>Input: nums = [0,0,1,1,1,2,2,3,3,4] </li>
    <li>Output: 5</li>
    <li>nums = [0,1,2,3,4,_,_,_,_,_]</li>
    <li>Explanation : Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
    It does not matter what you leave beyond the returned k (hence they are underscores) </li>
</ul>

#### <b style="color:Aqua"> Logic : </b>

1. We only want a single occurence of a number.
2. We can take two variables i & j. i is the index of next unique element & j is the iterator.
3. Initially i = 1 & j = 1 because the first element is always unique.
4. We will check if arr[j] > arr[i-1] because in the i-1 th index the last unique value is present and arr\[j\] will be unique if it is greater than arr[i-1]

#### <b style="color:Aqua">Code : </b>

```cpp
int i = 1;
    for(int j = 1; j < nums.size(); j++) {
        if(nums[j] > nums[i-1]) {
            nums[i++] = nums[j];
        }
    }       
return i;
```

---

### <span style = "color:violet">Question 5 - </span> [Link]()

#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet"> Question 13 & 14  </span>

#### <span style = "color:violet">Longest subarray with sum K (Positives + Negatives) - </span> [Link](https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=longest-sub-array-with-sum-k)

#### <span style = "color:violet"> Longest subarray with sum K (Positives & Zero) - </span>  [Link](https://www.naukri.com/code360/problems/longest-subarray-with-sum-k_6682399)

#### <b style="color:Aqua"> Problem Statement : </b>

Given an array containing N integers and an integer K., Your task is to find the length of the longest Sub-Array with the sum of the elements equal to the given value K.

#### <b style="color:Aqua"> Logic : </b>

<b>Brute Force : </b>
Generate all the sub arrays by using 2 nested loops and check the sum.

<b>Better : </b> (This is the optimal for Positives + Negatives)

<ol type=1>
<li> Keep a track of all the previous sum of the sub arrays in a Hashmap along with the index. </li>
<li> If at any point the sum is equal to K then that is the longest sub array till now. </li>
<li> If at any point the sum is x, then we should look in the map if there exist a sum (x-K). If exist calculate the length & compare </li>
<li> As we need the longest subarray we need the (x-K) to be as left as possible. So do not overwrite the index of an existing sum in the map.</li>
</ol>

<b>Optimal :</b>

<ol type=1>
<li> Keep a left & right pointer. Increase the right pointer while sum <= K. </li>
<li> When sum > K decrease the left pointer while sum <= K. </li>
<li> Continue the process until right == arr.size </li>
</ol>

#### <b style="color:Aqua">Code : </b>

```cpp {"id":"01HZVBM0AEWFZQJ9PNDGNR227K"}
// For Postive + Negative numbers

for(int i = 0; i < N ; i++) {
           sum += A[i];
           
           if(sum == K) {
                 maxLen = i+1;
           }
           else {
                int rem = sum - K;
                if(mp.find(rem) != mp.end()) {
                    int len = i - mp[rem];
                    maxLen = max(len,maxLen);
                }
           }
           
           if(mp.find(sum) == mp.end()) {
                  mp[sum] = i;
           }
}

// For Positive + Zero

while(j < arr.size()) {
       sum += arr[j];

       while(sum > k) {
         sum -= arr[i];
         i++;
       }

       if(sum == k) {
         maxLen = max(maxLen, j-i+1);
       }

       j++;
}
```

---






#  <span id="medium" style = "color:orange"> Medium </span> &nbsp;  [<span style = "font-size:10px; color:green;"> Easy</span>](#easy) &nbsp; [<span style = "font-size:10px;color:red;">Hard</span>](#hard)


### <span style = "color:violet">Question 1 - </span> [Link]()

#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 2 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 3 - Majority Element (>n/2 times) - </span> [Link](https://leetcode.com/problems/majority-element/)
#### <b style="color:Aqua"> Problem Statement : </b>  Given an array nums of size n, return the majority element. The majority element is the element that appears more than ⌊n / 2⌋ times.

#### <b style="color:Aqua"> Logic : </b>

<b>Brute Force : </b>
Use two nested loops & check for every element in the array if it is the majority element.

<b>Better : </b>
Use a Hashmap & store the frequency of every element in the array. If the frequency is greater than ⌊n / 2⌋ then it is the majority element.

<b>Optimal : </b>
<ol type=1>
<li> Use Moore's Voting Algorithm. </li>
<li> When count == 0 set the element to be nums[i] & count = 1. </li>
<li> If nums[i] == element then count++ else count-- </li>
<li> Continue the process  </li>
<li> Return the element if problem states there is always one majority elements </li>
<li> Otherwise check the element. If it appears more than ⌊n / 2⌋ times return it. If not the array has no majority element </li>
</ol>


#### <b style="color:Aqua">Code : </b>

```cpp
       int count = 0;
       int element;
        
       for(int i = 0; i < nums.size(); i++) {
           if(count == 0) {
              element = nums[i];
              count = 1;
           }
           else if(nums[i] == element) count++;
           else count--;
       }
        
       return element;

    // If there is possibility of no majority element check the element for majority
       int count1 = 0;
       for(int i = 0; i < nums.size(); i++) {
           if(nums[i] == element) count1++;
       }

       if(count1 > nums.size()/2) return element;

       return -1;

```

---

### <span style = "color:violet">Question 4 - Maximum Subarray (Kadane's Algorithm) - </span> [Link](https://leetcode.com/problems/maximum-subarray/)
#### <b style="color:Aqua"> Problem Statement : </b> Given an integer array nums, find the subarray with the largest sum, and return its sum.

#### <b style="color:Aqua"> Logic : </b>

<b>Brute Force : </b>
Use two nested loops & check for every subarray. Return the maximum sum.

<b>Optimal : </b>
<ol type=1>
<li> Use Kadane's algorithm. </li>
<li> Initialize sum = 0, maxi = INT_MIN. </li>
<li> We do not carry any negative sum forward because it will hamper my result in future. So, if sum < 0 then set sum = 0 </li>
<li> Update maxi = max(maxi, sum) </li>
<li> Return maxi </li>
<li> If problem states including empty subarray then return max(0, maxi) </li>
</ol>

#### <b style="color:Aqua">Code : </b>

```cpp
        int sum = 0;
        int maxi = INT_MIN;
        
        for(int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            
            if(sum > maxi) {
              maxi = sum;
            }
            
            if(sum < 0) {
               sum = 0;
            }
        }
        
       return maxi;

```

---

### <span style = "color:violet">Question 5 - Print subarray with maximum subarray sum (extended version of the above problem) </span>
#### <b style="color:Aqua"> Problem Statement : </b> Given an integer array nums, find the subarray with the largest sum, and return the subarray. If there is multiple subarrays with the largest sum, return any of them.

#### <b style="color:Aqua"> Logic : </b>
<ol type=1>
<li> Use Kadane's algorithm Like the above problem </li>
<li> Initialize start variable to i, wherever sum = 0 </li>
<li> When sum > maxSum, update the ansStart with start & ansEnd with i </li>
</ol>

#### <b style="color:Aqua">Code : </b>

```cpp
        int sum = 0;
        int maxi = INT_MIN;
        int start = -1, ansStart = -1, ansEnd = -1;

        for(int i = 0; i < nums.size(); i++) {
            if(sum == 0) start = i;
            sum += nums[i];
            
            if(sum > maxi) {
              maxi = sum;
              ansStart = start;
              ansEnd = i;
            }
            
            if(sum < 0) {
               sum = 0;
            }
        }
        
       // return the subarray from ansStart to ansEnd

```

---

### <span style = "color:violet">Question 6 - Stock Buy and Sell - </span> [Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
#### <b style="color:Aqua"> Problem Statement : </b> You are given an array prices where prices[i] is the price of a given stock on the ith day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

#### <b style="color:Aqua"> Logic : </b>
If I want to sell a stock on the ith day, I should buy the stock on the minimum from 0 to i-1th day.
So I need to keep a track of minimum price for every index.

#### <b style="color:Aqua">Code : </b>

```cpp
       int buy = prices[0];
       int profit = 0;
        
        for(int i = 1; i < prices.size(); i++) {
          profit = max(profit,prices[i]-buy);
          buy = min(buy,prices[i]);
        }
        
       return profit;

```

---

### <span style = "color:violet">Question 7 - Rearrange Array Elements by Sign - </span> [Link](https://leetcode.com/problems/rearrange-array-elements-by-sign/)
#### <b style="color:Aqua"> Problem Statement : </b>  You are given a 0-indexed integer array nums of even length consisting of an equal number of positive and negative integers. You should return the array of nums such that the the array follows the given conditions :

#### 1. Every consecutive pair of integers have opposite signs.
#### 2. For all integers with the same sign, the order in which they were present in nums is preserved.
#### 3. The rearranged array begins with a positive integer.

#### Return the modified array after rearranging the elements to satisfy the aforementioned conditions.


#### <b style="color:Aqua"> Logic : </b>

<b>Brute Force : </b>
<ol type=1>
<li> Take 2 arrays of n/2 size to store positive and negative numbers respectively. </li>
<li> Put all the positive numbers in the first array and negative numbers in the second array. </li>
<li> Positive Numbers go to the even indexes & Negative numbers go to the odd indexes.</li>
<li> For that reason positive numbers will go to arr[2*i] & negative numbers will go to arr[2*i+1]</li>
</ol>

<b>Optimal : </b>

<ol type=1>
<li> Positive Numbers go to the even indexes & Negative numbers go to the odd indexes. </li>
<li> Initially, take positiveIndex = 0 & negativeIndex = 1 </li>
<li> Take an extra array ans of size n </li>
<li> If the number is positve, put the number in ans[positiveIndex] & do positiveIndex += 2 </li> 
<li> If the number is negative, put the number in ans[negativeIndex] & do negativeIndex += 2</li>
</ol>

#### <b style="color:Aqua">Code : </b>

```cpp
// Brute Force
    // Assuming pos is the array of postive numbers and neg is the array of negative numbers
    int n = nums.size();
    for(int i = 0; i < n/2; i++) {
       nums[2*i] = pos[i];
       nums[2*i+1] = neg[i]; 
    }

// Optimal

        int pos = 0, neg = 1;
        vector<int> ans(nums.size(),0);
            
        for(int i = 0 ; i < nums.size(); i++) {
            if(nums[i] > 0) {
            ans[pos] = nums[i];
            pos += 2;
            }
            else {
            ans[neg] = nums[i];
            neg += 2;
            }
        }
            
        return ans;

```
#### <b style="color:Aqua">Follow Up Question : </b> We are not sure that the number of postive integer & negative integer is equal. Can we do it in optimal way?

#### <b style="color:Aqua"> Logic : </b>
<ol type=1>
<li> Fall Back to the brute force approach </li>
<li> Take 2 arrays of n/2 size to store positive and negative numbers respectively. </li>
<li> Put all the positive numbers in the first array and negative numbers in the second array. </li>
<li> Positive Numbers go to the even indexes & Negative numbers go to the odd indexes.</li>
<li> For that reason positive numbers will go to arr[2*i] & negative numbers will go to arr[2*i+1]</li>
<li> Whatever is left, store it as it is in the main array</li>
</ol>

#### <b style="color:Aqua">Code : </b>

```cpp
    int n = nums.size();
    if(pos.size() > neg.size()) {
        for(int i = 0; i < neg.size(); i++) {
            nums[2*i] = pos[i];
            nums[2*i+1] = neg[i]; 
        }
        int index = 2*neg.size();
        for(int i = neg.size(); i < pos.size(); i++) {
            nums[index] = pos[i];
            index++;
        }
    }
    else {
        for(int i = 0; i < pos.size(); i++) {
            nums[2*i] = pos[i];
            nums[2*i+1] = neg[i]; 
        }
        int index = 2*pos.size();
        for(int i = pos.size(); i < neg.size(); i++) {
            nums[index] = neg[i];
            index++;
        }  
    }

```

---

### <span style = "color:violet">Question 8 - Next Permutation - </span> [Link](https://leetcode.com/problems/next-permutation/)
#### <b style="color:Aqua"> Problem Statement : </b> Given an array of integers nums, find the next permutation of nums. The replacement must be in place and use only constant extra memory. 
The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).
<ul>
<li>For example, the next permutation of arr = [1,2,3] is [1,3,2]. </li>
<li> Similarly, the next permutation of arr = [2,3,1] is [3,1,2]. </li>
<li> While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement. </li>
</ul>

#### <b style="color:Aqua"> Logic : </b>
<b> Brute Force : </b>
<ol type=1>
<li> Generate all the permutations of the array and sort them. </li>
<li> Do a linear search & return the next permutation </li>
<li> If the given array is the last permutation, return the first permutation</li>
</ol>

<b> Better : </b>
<ol type=1>
<li> Use STL function next_permutation </li>
<li> That will modify the existing array in place </li>
</ol>

<b>Optimal : </b>
<ol type=1>
<li> Find a break point where nums[i] < nums[i+1] from the back. The last break point can be n-2. So, start from n-2 </li>
<li> If there is no break point, it means it is the last permutation. So just reverse the array and return it </li>
<li> So, index i is the break point. Now find an element in the right part that is greater than nums[i] but smallest. Now swap them and break the loop</li>
<li> Now sort the right part from index i+1. As it is already sorted in reverse order. We can just reverse it</li>
<li> Take example of [2,1,5,4,3,0,0] & dry run to better understand the algorithm </li>
</ol>

#### <b style="color:Aqua">Code : </b>

```cpp

      int breakPoint = -1;
      int n = nums.size();
        
      for(int i = n-2; i >= 0; i--) {
        if(nums[i] < nums[i+1]) {
            breakPoint = i;
            break;
        }
      }
        
      if(breakPoint == -1) {
        reverse(nums.begin(),nums.end());
        return;
      }
        
      for(int i = n-1; i > breakPoint; i--) {
         if(nums[i] > nums[breakPoint]) {
            swap(nums[i],nums[breakPoint]);
            break;
         }
      }
        
      reverse(nums.begin() + breakPoint + 1, nums.end());
```

---

### <span style = "color:violet">Question 9 - Leaders in an Array - </span> [Link](https://www.geeksforgeeks.org/problems/leaders-in-an-array-1587115620/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=leaders-in-an-array)
#### <b style="color:Aqua"> Problem Statement : </b> Given an array arr[] of n positive integers. Your task is to find the leaders in the array. An element of the array is a leader if it is greater than all the elements to its right side or if it is equal to the maximum element on its right side. The rightmost element is always a leader. 

#### <b style="color:Aqua"> Logic : </b>
<b> Brute Force : </b>
<ol type=1>
<li> Take two nested loops</li>
<li> Check for every element if it is greater than or equal to the largest element on the right side</li>
</ol>

<b>Optimal : </b>
<ol type=1>
<li> Traverse the array from right to left</li>
<li> Keep the track of maximum element of the right side </li>
<li> Compare each element with the maximum element</li>
<li> Reverse the array at the end to maintain the order of the elements</li>
</ol>

#### <b style="color:Aqua">Code : </b>

```cpp
       vector<int> ans;
       int maxi = INT_MIN;
       
       for(int i = n-1; i >= 0; i--) {
          if(arr[i] >= maxi) {
            ans.push_back(arr[i]);
            maxi = arr[i];
          }
       }
       
       reverse(ans.begin(),ans.end());
       
       return ans;
```

---

### <span style = "color:violet">Question 10 - Longest Consecutive Sequence in an Array - </span> [Link](https://leetcode.com/problems/longest-consecutive-sequence/)
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 11 - Set Matrix Zeros - </span> [Link](https://leetcode.com/problems/set-matrix-zeroes/)
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 12 - Rotate Matrix by 90 degrees - </span> [Link](https://leetcode.com/problems/rotate-image/)
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 13 - Print the matrix in spiral manner - </span> [Link](https://leetcode.com/problems/spiral-matrix/)
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 14 - Count subarrays with given sum - </span> [Link](https://leetcode.com/problems/subarray-sum-equals-k/)
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---





#  <span id="hard" style = "color:red"> Hard </span>  &nbsp; [<span style = "font-size:10px;color:green;"> Easy</span>](#easy) &nbsp; [<span style = "font-size:10px;color:orange;">Medium</span>](#medium)



### <span style = "color:violet">Question 1 - </span> [Link]()

#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 2 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 3 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 4 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 5 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 6 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 7 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 8 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 9 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 10 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 11 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 12 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---
