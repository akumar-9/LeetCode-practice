# Top K Frequent Elements

# Problem Statement
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

### Example
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

## Approach
I use a frequency map, to count the occurrences of each element. Then use a min heap of size `k` to store the elements where I use the frequency as the priority. I will maintain the size `k` by pushing elements and popping if the count exceeds `k`. Finally convert the min heap to list. Another approach can be using bucket sort.
### Time Complexity
- **O(nlogk)**: n is length of nums. 
### Space Complexity
- **O(k)**: Min heap holds atmost k elements

## Solution Code
```C#
public class Solution {
    public int[] TopKFrequent(int[] nums, int k) {
        Dictionary<int,int> freqMap = new Dictionary<int,int>();
        foreach(int num in nums){
            if(!freqMap.ContainsKey(num)){
                freqMap[num]=0;
            }
            freqMap[num]++;
        }

        PriorityQueue<int,int> minHeap = new PriorityQueue<int,int>();
        foreach(KeyValuePair<int,int> pair in freqMap){
            minHeap.Enqueue(pair.Key, pair.Value);
            if(minHeap.Count > k){
                minHeap.Dequeue();
            }
        }

        int[] result = new int[k];
        for(int i = k-1; i>=0; i--){
            result[i]= minHeap.Dequeue();
        }
        return result;
    }

}