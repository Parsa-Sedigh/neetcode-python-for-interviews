## arr
```python
arr = [1, 2, 3]

# Since the lists in py are dynamic arrs and not stacks, we can insert into the middle. But unlike append() and pop() which are
# O(1), inserting into the middle is O(n) time op.
arr.insert(1, 7) # T: O(n)

# But indexing is not O(n)
arr[0] = 0 # O(1)

# initialize a list of variable size
n = 5
arr = [1] * n

# Be careful: -1 is not out of bounds, it's last value
print(arr[-1])

# Getting sublists(aka slicing a list)
# Note: Last index is non-inclusive
print(arr[1:3]) # not including index 3 in this case.
```

## Sorting
```python
arr = ["bob", "alice"]

# sorts based on alphabetical order
arr.sort()
print(arr)

# Custom sort(by length of string)
arr.sort(key=lambda x: len(x))
```

## List comprehension
```python
arr = [i for i in range(5)] # [0, 1, 2, 3, 4]

# build a 4 by 4(4x4) grid of all zeroes
# [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
arr = [[0] * 4 for i in range(4)]

# Technically this will also work. But each of the rows of this arr are going to be the same. So if we modify one of the rows,
# all of the other rows will be modified as well. This is because we're not creating four UNIQUE rows in this case.
arr = [[0] * 4] * 4
```

## strings
Strings are similar to arrays. But they are immutable, so we can't modify them. So this won't have any effect:
```python
s = "abc"
s[0]= "A"

# So this creates a new string:
# Note: Anytime you update a string, like here, it's considered a O(n) op because you're creating a new string that has
# the specified length.
s += "def" # O(n)
```

## queues
Queues in py are double ended queues by default.

## hash sets
```python
print(set[1, 2, 3])

# set comprehension
mySet = { i for i in range(5) }
print(mySet)
```

## HashMap(aka dict)
```python
myMap = {}

# dict comprehension
myMap = { i : 2*i for i in range(3)}

# There are many ways to loop through a map.

# By default, we iterate through every key and then we can get the value using that key
for key in myMap:
    print(key, myMap[key])

# If we don't need the key, we can directly loop through the list of vals:
for val in myMap.values():
    print(val)

for key, val in myMap.items():
    print(key, val)
```

## Tuples
Python has tuples which are similar to lists but immutable and to initialize them, we use parentheses rather than brackets. 
So while we can index them, we can't modify them.
```python
tup = (1, 2, 3)
print(tup[-1])

# Won't work:
tup[0] = 0
```

You'll mainly be using tuples as keys for a hashmap or hashset:
```python
# tuple as key in hashmap:
myMap = { (1, 2): 3 }
print(myMap[(1, 2)])

# tuple as key in hashset:
mySet = set()
mySet.add((1, 2))
print((1, 2) in mySet)
```

Why we do this?

Because lists are not hashable and can't be keys for hashsets or hashmaps, so this won't work:
```python
myMap = {}

myMap[[3, 4]] = 5
```

## heaps
To find min and max of a set of values. Under the hood in py, they are implemented with arrs. By default, heaps in py are min-heaps.

No max heaps by default in py. The workaround is to multiply each value that we wanna push by -1 and then after we pop it, 
we multiply it by -1 again to negate the original -1.

```python
import heapq

maxHeap = []
heapq.heappush(maxHeap, -3)
heapq.heappush(maxHeap, -2)

# max is always at index 0
print(-1 * maxHeap[0])  # 4 which is the maximum value of the list

# values are printed from greatest to smallest(max-heap)
while maxHeap:
    print(-1 * heapq.heappop(maxHeap))
```

If you already have the initial set of values, you can do it in O(n):

```python
import heapq

arr = [2, 4, 3]

heapq.heapify(arr)

while arr: # from smallest to largest
    print(heapq.heappop(arr))
```

## nested functions
In nested funcs, you can modify objs but you can't reassign values unless you use the `nonlocal` keyword.

So if you want to update the value outside of the nested func, declare it as a non local value. Doing this will update the value.

```python
# doubles arr and val
def double(arr, val):
    def helper():
        # modifying array works
        for i, n in enumerate(arr):
            arr[i] *= 2

        # will only modify val in the helper func scope:
        # val *= 2

        # this will modify val outside helper func scope:
        nonlocal val
        val *= 2

    helper()
    print(arr, val)


double([1, 2], 3)
```