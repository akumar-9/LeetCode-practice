# Find Median from Data Stream

# Problem Statement
The median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value, and the median is the mean of the two middle values.

- For example, for `arr = [2,3,4]`, the median is `3`.
- For example, for `arr = [2,3]`, the median is `(2 + 3) / 2 = 2.5`.
Implement the MedianFinder class:

- `MedianFinder()` initializes the MedianFinder object.
- `void addNum(int num)` adds the integer num from the data stream to the data structure.
- `double findMedian()` returns the median of all elements so far. Answers within 10-5 of the actual answer will be accepted.


### Example
Input
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
Output
[null, null, null, 1.5, null, 2.0]


## Approach
If you take a look carefully, median is in the middle of a sorted list. So if data is recieved not all at once, but instead as a stream, what's the best data structure that keeps the sorted order ? Heaps, right? You could also use insertion sort. But for the heaps approach, how do you know which is the middle element, well you can break the final at the middle, then you would have two lists. You can make one of them min heap and other max heap. If the smaller half of the list is stored in a max heap, then we can get the middle element in o(1) because it will be the top of max-heap. Similarly, if the larger half of the list is stored in a min heap, then we can get the middle element in O(1). At any point the max heap will have atmost 1 or more element that min-heap.
### Time Complexity
- **O(log n)**: Adding a num to heap and O(1) for finding median
### Space Complexity
- **O(n)**: space taken by both the heaps is atmost n
## Solution Code
```C#
public class MedianFinder {
    PriorityQueue<int,int> minHeap;
    PriorityQueue<int,int> maxHeap;
    public MedianFinder() {
        minHeap = new PriorityQueue<int,int>();
        maxHeap = new PriorityQueue<int,int>(Comparer<int>.Create((a,b) => b.CompareTo(a)));
    }
    
    public void AddNum(int num) {
       maxHeap.Enqueue(num, num);
        int val = maxHeap.Dequeue();
        minHeap.Enqueue(val,val);
       if(maxHeap.Count < minHeap.Count){
        val = minHeap.Dequeue();
        maxHeap.Enqueue(val,val);
        
       }
    }
    
    public double FindMedian() {
        
        if(maxHeap.Count == minHeap.Count){
            return ( maxHeap.Peek() + minHeap.Peek() ) / 2.0;
        }
        return maxHeap.Peek();
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.AddNum(num);
 * double param_2 = obj.FindMedian();
 */