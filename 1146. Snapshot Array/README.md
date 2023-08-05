
###### tags:
HashTable, Array, String
###### date: 

[leetcode link](https://leetcode.com/problems/snapshot-array/)

## **Description**

Implement a SnapshotArray that supports the following interface:

SnapshotArray(int length) initializes an array-like data structure with the given length. Initially, each element equals 0.
void set(index, val) sets the element at the given index to be equal to val.
int snap() takes a snapshot of the array and returns the snap_id: the total number of times we called snap() minus 1.
int get(index, snap_id) returns the value at the given index, at the time we took the snapshot with the given snap_id

#### Constraints

1 <= length <= 5 * 104
0 <= index < length
0 <= val <= 109
0 <= snap_id < (the total number of times we call snap())
At most 5 * 104 calls will be made to set, snap, and get.

## **Solution**

### Approach 1: 

##### Code:

```java
class SnapshotArray {

    
    TreeMap<Integer, Integer>[] trees; 
    int snapId; 
    public SnapshotArray(int length) {
        trees = new TreeMap[length];
        for(int i = 0; i < length; i ++){
            trees[i] = new TreeMap<Integer, Integer>();
            trees[i].put(0,0);
        }
    }
    
    public void set(int index, int val) {
        trees[index].put(snapId, val);
    }
    
    public int snap() {
        return snapId ++; 
    }
    
    public int get(int index, int snap_id) {
        return trees[index].floorEntry(snap_id).getValue();
        
    }
}

/**
 * Your SnapshotArray object will be instantiated and called as such:
 * SnapshotArray obj = new SnapshotArray(length);
 * obj.set(index,val);
 * int param_2 = obj.snap();
 * int param_3 = obj.get(index,snap_id);
 */
```

##### Complexity:

##### Time
SnapshotArray(int length): This function has a time complexity of O(n), where n is the length of the array. It has to initialize a TreeMap for each index in the array.

set(int index, int val): The time complexity of this operation is O(log m), where m is the number of snapshots taken for the specific index. The put operation in a TreeMap has a logarithmic time complexity because TreeMap is a Red-Black Tree based NavigableMap implementation in Java and all important operations including put and get take logarithmic time.

snap(): The time complexity of the snap() operation is O(1), because it only involves returning and incrementing the current snapshot id.

get(int index, int snap_id): The time complexity is O(log m), where m is the number of snapshots taken for the specific index. The floorEntry operation in a TreeMap is a logarithmic operation.


##### Space
The space complexity of the SnapshotArray is O(n*m), where n is the number of indices and m is the number of snapshots, as it stores a history of values for each index for each snapshot.

## **Reference**