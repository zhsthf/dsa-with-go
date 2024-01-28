
# GO Arrays

## Introduction
In the Go programming language, an array is a numbered sequence of elements of a specific length. Arrays are useful when you need a fixed number of elements of the same type.

## Declaring Arrays
An array is declared by specifying the type of its elements and the number of elements it will hold.

```go
var myArray [5]int
```

## Initializing Arrays
Arrays can be initialized in various ways.

### Method 1: Individual Element Assignment
```go
myArray[0] = 1
myArray[1] = 2
// ... and so on
```

### Method 2: Declaration with Initialization
```go
myArray := [5]int{1, 2, 3, 4, 5}
```

### Method 3: Using the `...` Operator
```go
myArray := [...]int{1, 2, 3, 4, 5}
```

## Accessing Array Elements
Access elements by their index, which starts at 0.

```go
fmt.Println("First element:", myArray[0])
fmt.Println("Second element:", myArray[1])
```

## Iterating Over Arrays
Use a `for` loop to iterate over array elements.

```go
for i, v := range myArray {
    fmt.Printf("Index: %d, Value: %d
", i, v)
}
```

## Common Methods and Functions for Arrays

### Length of an Array
Use the `len()` function to find the length of an array.

```go
length := len(myArray)
fmt.Println("Length of the array:", length)
```

### Copying an Array
To copy an array, use the `copy()` function.

```go
var arrayCopy [5]int
copy(arrayCopy[:], myArray[:])
fmt.Println("Copied Array:", arrayCopy)
```

### Converting an Array to a Slice
Arrays can be converted to slices, which are more flexible.

```go
mySlice := myArray[:]
```

### Looping Through an Array
Besides the `range` form, you can use a traditional `for` loop.

```go
for i := 0; i < len(myArray); i++ {
    fmt.Println(myArray[i])
}
```

## Multidimensional Arrays
Go supports multidimensional arrays.

```go
var matrix [3][3]int
matrix[0] = [3]int{1, 2, 3}
matrix[1] = [3]int{4, 5, 6}
matrix[2] = [3]int{7, 8, 9}
```

### Example: Initializing a 2D Array
```go
var matrix [3][3]int = [3][3]int{{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}
```

### Example: 3D Array
```go
var threeD [2][3][4]int
```

## Advanced Slicing
Slicing can be used to manipulate arrays in complex ways.

### Example: Slicing a Multi-Dimensional Array
```go
slice := matrix[1:3][1:2]
```

## Array Algorithms
Understanding common algorithms can enhance how you use arrays.

### Sorting
Go's standard library provides sorting for slices, but you can implement sorting for arrays.

#### Example: Bubble Sort
```go
func bubbleSort(arr [5]int) [5]int {
    n := len(arr)
    for i := 0; i < n; i++ {
        for j := 0; j < n-i-1; j++ {
            if arr[j] > arr[j+1] {
                arr[j], arr[j+1] = arr[j+1], arr[j]
            }
        }
    }
    return arr
}
```

### Searching
Implement common searching algorithms for arrays.

#### Example: Binary Search
```go
func binarySearch(arr [5]int, x int) int {
    low, high := 0, len(arr)-1
    for low <= high {
        mid := low + (high-low)/2
        if arr[mid] == x {
            return mid
        } else if arr[mid] < x {
            low = mid + 1
        } else {
            high = mid - 1
        }
    }
    return -1
}
```

## Example: Full Program
Here's a full example program that demonstrates some of these concepts.

```go
package main

import "fmt"

func main() {
    var a [5]int
    fmt.Println("emp:", a)

    a[4] = 100
    fmt.Println("set:", a)
    fmt.Println("get:", a[4])

    fmt.Println("len:", len(a))

    b := [5]int{1, 2, 3, 4, 5}
    fmt.Println("dcl:", b)

    var twoD [2][3]int
    for i := 0; i < 2; i++ {
        for j := 0; j < 3; j++ {
            twoD[i][j] = i + j
        }
    }
    fmt.Println("2d: ", twoD)
}
```
