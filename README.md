Here are examples of various time complexities with PHP:

### 1.  **O(1) - Constant Time Complexity:**
   ```php
   function constantTimeExample($array) {
       return $array[0];
   }
   ```

### 2.  *O(log n) - Logarithmic Time Complexity (Binary Search):*
   ```php
   function binarySearch($array, $target) {
       $low = 0;
       $high = count($array) - 1;
       
       while ($low <= $high) {
           $mid = floor(($low + $high) / 2);
           
           if ($array[$mid] === $target) {
               return $mid;
           } elseif ($array[$mid] < $target) {
               $low = $mid + 1;
           } else {
               $high = $mid - 1;
           }
       }
       
       return -1;
   }
   ```

Suppose you have a sorted array:

```php
$array = [2, 4, 7, 11, 16, 21, 25, 30];
```

Now, let's use the `binarySearch` function to find the index of the target value `16`:

```php
$target = 16;
$result = binarySearch($array, $target);
```

**Explanation of Steps:**

1. **Initialization:**
    - `$low` is initially set to `0`.
    - `$high` is initially set to `7` (the index of the last element).

2. **First Iteration:**
    - Calculate the middle index: `$mid = floor((0 + 7) / 2) = 3`.
    - Compare `$array[3]` (value `11`) with the target (`16`).
    - Since `11` is less than `16`, update `$low` to `$mid + 1` (setting `$low` to `4`).

3. **Second Iteration:**
    - Calculate the middle index: `$mid = floor((4 + 7) / 2) = 5`.
    - Compare `$array[5]` (value `21`) with the target (`16`).
    - Since `21` is greater than `16`, update `$high` to `$mid - 1` (setting `$high` to `4`).

4. **Third Iteration:**
    - Calculate the middle index: `$mid = floor((4 + 4) / 2) = 4`.
    - Compare `$array[4]` (value `16`) with the target (`16`).
    - The values are equal, so the function returns `$mid`, which is `4`.

**Result:**
The index of the target value `16` in the array is `4`. Therefore, the output of the function will be `4`.   


### 3.  **O(n) - Linear Time Complexity:**
   ```php
   function linearTimeExample($array) {
       foreach ($array as $element) {
           // Some operation with each element
           echo $element;
       }
   }
   ```

### 4.  **O(n log n) - Linearithmic Time Complexity (Merge Sort):**
   ```php
   function mergeSort($array) {
       if (count($array) <= 1) {
           return $array;
       }

       $mid = count($array) / 2;
       $left = array_slice($array, 0, $mid);
       $right = array_slice($array, $mid);

       $left = mergeSort($left);
       $right = mergeSort($right);

       return merge($left, $right);
   }

   function merge($left, $right) {
       $result = [];
       while (count($left) > 0 && count($right) > 0) {
           if ($left[0] <= $right[0]) {
               array_push($result, array_shift($left));
           } else {
               array_push($result, array_shift($right));
           }
       }

       while (count($left) > 0) {
           array_push($result, array_shift($left));
       }

       while (count($right) > 0) {
           array_push($result, array_shift($right));
       }

       return $result;
   }
   ```

```php
$array = [38, 27, 43, 3, 9, 82, 10];
$result = mergeSort($array);
```

**Explanation of Steps:**

1. **Input Array:**
   ```php
   $array = [38, 27, 43, 3, 9, 82, 10];
   ```

2. **Initial Call to `mergeSort`:**
    - The array is split into two halves: `[38, 27, 43]` and `[3, 9, 82, 10]`.
    - Each half is recursively sorted using `mergeSort`.

3. **Recursive Sorting of Left Half:**
    - `[38, 27, 43]` is further split into `[38]`, `[27]`, and `[43]`.
    - The individual elements are considered sorted.

4. **Recursive Sorting of Right Half:**
    - `[3, 9, 82, 10]` is split into `[3, 9]` and `[82, 10]`.
    - Further split into `[3]`, `[9]`, `[82]`, and `[10]`.

5. **Merging:**
    - The sorted halves are merged back together.
    - `[38, 27, 43]` and `[3, 9, 82, 10]` are merged into a sorted array: `[3, 9, 10, 27, 38, 43, 82]`.

**Result:**
The result of applying the `mergeSort` function to the input array is a sorted array:

```php
$result = [3, 9, 10, 27, 38, 43, 82];
```

The time complexity of merge sort is O(n log n), and this example demonstrates how the algorithm divides and conquers the array to achieve a sorted result.

### 5.  **O(n^2) - Quadratic Time Complexity (Bubble Sort):**
   ```php
   function bubbleSort($array) {
       $n = count($array);
       for ($i = 0; $i < $n - 1; $i++) {
           for ($j = 0; $j < $n - $i - 1; $j++) {
               if ($array[$j] > $array[$j + 1]) {
                   // Swap $array[$j] and $array[$j + 1]
                   $temp = $array[$j];
                   $array[$j] = $array[$j + 1];
                   $array[$j + 1] = $temp;
               }
           }
       }
       return $array;
   }
   ```


```php
$array = [64, 34, 25, 12, 22, 11, 90];
$result = bubbleSort($array);
```

**Explanation of Steps:**

1. **Input Array:**
   ```php
   $array = [64, 34, 25, 12, 22, 11, 90];
   ```

2. **First Pass:**
    - In the first pass, the largest element (`90`) is bubbled to the end of the array.
    - Comparisons and swaps are made between adjacent elements.

   ```php
   Pass 1:
   [34, 25, 12, 22, 11, 64, 90]
   ```

3. **Second Pass:**
    - In the second pass, the second-largest element (`64`) is bubbled to the second-to-last position.

   ```php
   Pass 2:
   [25, 12, 22, 11, 34, 64, 90]
   ```

4. **Third Pass:**
    - The process continues, and each pass moves the next largest unsorted element into its correct position.

   ```php
   Pass 3:
   [12, 22, 11, 25, 34, 64, 90]
   ```

   ```php
   Pass 4:
   [12, 11, 22, 25, 34, 64, 90]
   ```

   ```php
   Pass 5:
   [11, 12, 22, 25, 34, 64, 90]
   ```

5. **Final Result:**
    - After the required number of passes, the array is sorted.

   ```php
   Final Sorted Array:
   [11, 12, 22, 25, 34, 64, 90]
   ```

**Result:**
The result of applying the `bubbleSort` function to the input array is a sorted array:

```php
$result = [11, 12, 22, 25, 34, 64, 90];
```

Bubble sort has a time complexity of O(n^2) because it involves nested loops, and the number of comparisons and swaps grows quadratically with the size of the input array.

These examples illustrate different time complexities in PHP algorithms. Keep in mind that actual performance can depend on various factors, and these are simplified representations for educational purposes.