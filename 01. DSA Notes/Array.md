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

#### <span style = "color:violet">Longest subarray with sum K (Positives + Negatives) </span> [Link](https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=longest-sub-array-with-sum-k)

#### <span style = "color:violet"> Longest subarray with sum K (Positives & Zero) </span>  [Link](https://www.naukri.com/code360/problems/longest-subarray-with-sum-k_6682399)

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

### <span style = "color:violet">Question 13 - </span> [Link]()
#### <b style="color:Aqua"> Problem Statement : </b>

#### <b style="color:Aqua"> Logic : </b>

#### <b style="color:Aqua">Code : </b>

```cpp


```

---

### <span style = "color:violet">Question 14 - </span> [Link]()
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
