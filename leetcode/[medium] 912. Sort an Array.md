# Title
[912. Sort an Array] (https://leetcode.com/problems/sort-an-array/)

# Description
Given an array of integers nums, sort the array in ascending order.

# Example 1:

    Input: [5,2,3,1]
    Output: [1,2,3,5]

# Example 2:

    Input: [5,1,1,2,0,0]
    Output: [0,0,1,1,2,5]
 

# Note:

* 1 <= A.length <= 10000
* -50000 <= A[i] <= 50000

# Solution

## Quick Sort
    class Solution {
        public int[] sortArray(int[] nums) {
            quickSort(nums, 0, nums.length);
        }

        private void quickSort(int[] nums, int start, int end) {
            int diff = end - start;
            if (diff <= 12) {
                insertSort(nums, start, end);
                return;
            }

            int partition = partition(nums, start, end);
            quickSort(nums, start, partition - 1);
            quickSort(nums, partition + 1, end);
        }

        private int partition(int[] nums, int start, int end) {
            int less = start;
            for (int i = start; i <= end; i++) {
                if (isLess(nums, i, end)) {
                    exchange(nums, less, i);
                    less++;
                }
            }

            exchange(nums, less, end);
            return less;
        }

        private int[] insertSort(int[] nums, int start, int end) {
            for (int i = start; i <= end; i++) {
                for (int j = i; j > start && isLess(nums, j, j - 1); j--) {
                    exchange(nums, j, j - 1);
                }
            }

            return nums;
        }
    }
    
## Merge Sort
        class Solution {
            public int[] sortArray(int[] nums) {
                    mergeSort(nums, 0, nums.length -1);
                    return nums;
            }

            private void mergeSort(int[] nums, int low, int high) {
                if (low >= high) {
                        return;
                }
                int mid = (low + high) / 2;
                mergeSort(nums, low, mid);
                mergeSort(nums, mid + 1, high);
                merge(nums, low, mid + 1, high);
            }

            private void merge(int[] nums, int low, int mid, int high) {
                int lLength = mid - low;
                int rLength = high - mid + 1;
                int[] left = new int[lLength];
                int[] right = new int[rLength];
                System.arraycopy(nums, low, left, 0, lLength);
                System.arraycopy(nums, mid, right, 0, rLength);
                int l = 0, r = 0, i = low;
                while (l < lLength && r < rLength) {
                    nums[i++] = left[l] < right[r] ? left[l++] : right[r++];
                }

                while (l < lLength) {
                    nums[i++] = left[l++];
                }

                while (r < rLength) {
                    nums[i++] = right[r++];
                }
            }
            // There is drawback in this method
            private void merge1(int[] nums, int low, int mid, int high) {
                // copy to auxi array
                int length = high - low + 1;
                int[] auxi = new int[length];

                int left = low, right = mid;
                int i = 0;
                while (i < length && left < mid && right < high) {
                        if (nums[left] < nums[right]) {
                                auxi[i] = nums[left++];
                        } else {
                                auxi[i] = nums[right++];
                        }
                        i++;
                }
                if (right == high) {
                        System.arraycopy(nums, left, auxi, i, mid - left);
                } else {
                        System.arraycopy(nums, right, auxi, i, high - right + 1);
                }
                // copy item back in ascending order.
                System.arraycopy(auxi, 0, nums, low, length);
            }
        }

## HeapSort
        class Solution {
            public int[] sortArray(int[] nums) {
                return sortByHeap(nums);
            }

            private int[] sortByHeap(int[] nums) {
                int length = nums.length;
                int heapIndex = length - 1;
                // shift right one bit is equivalent to divide to 2, don't shift two bit by mistake.
                for (int i = heapIndex >> 1; i >= 0; i--) {
                    maxHeapRecursive(nums, i, heapIndex);
                }

                for (int i = 0; i < length; i++) {
                    System.out.print(nums[i] + ", ");
                }

                while (heapIndex > 0) {
                    exchange(nums, 0, heapIndex);
                    --heapIndex;
                    maxHeapRecursive(nums, 0, heapIndex);
                }

                return nums;
            }

            private void maxHeapRecursive(int[] nums, int i, int heapIndex) {
                int left = 2 * i + 1;
                int right = 2 * i + 2;
                int max = i;
                if (left <= heapIndex && nums[left] > nums[i]) {
                    max = left;
                }

                if (right <= heapIndex && nums[right] > nums[max]) {
                    max = right;
                }

                if (max != i) {
                    exchange(nums, max, i);
                    maxHeapRecursive(nums, max, heapIndex);
                }
            }

            private void exchange(int[] nums, int i, int j) {
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
            }
        }
        
## Insert Sort
        class Solution {
            public int[] sortArray(int[] nums) {
                return insertSort(nums);
            }

            /**
             * Insertion sort works the way many people sort a hand of playing cards. 
             * which starts with an empty left hand and the cards face down on the table. 
             * We remove one card at a time from the table and insert it into the correct
             * position in the left hand. To find the correct position for a card, we
             * compare it with each card in the hand, from right to left.
             */
            private int[] insertSort(int[] nums) {
                int length = nums.length;
                for (int i = 1; i < length; i++) {
                    int key = nums[i];
                    for (int j = i; j > 0 && isLess(nums, j, j - 1); j--) {
                        exchange(nums, j, j - 1);
                    }
                }

                return nums;
            }

            private boolean isLess(int[] nums, int i, int j) {
                return nums[i] < nums[j];
            }

            private void exchange(int[] nums, int i, int j) {
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
            }
        }
        
## Select Sort
        class Solution {
            public int[] sortArray(int[] nums) {
                return selectSort(nums);
            }

            /**
             * First, find the smallest item in the array and exchange it with the first
             * entry. Then, find the next smallest item and exchange it with the second 
             * entry. Continue in this way, until the entire array is sorted. This method
             * is called selection sort because it works by repeatedly selecting the 
             * smallest remaining item.
             **/
            private int[] selectSort(int[] nums) {
                int length = nums.length;
                for (int i = 0; i < length - 1; i++) {
                    int smallest = i;
                    for (int j = i + 1; j < length; j++) {
                        if (nums[j] < nums[smallest]) {
                            smallest = j;
                        }
                    }
                    exchange(nums, i, smallest); 
                }
                return nums;
            }

            private void exchange(int[] nums, int i, int j) {
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
            }
        }
