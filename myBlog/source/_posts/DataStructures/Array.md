# **Ⅰ. Array Data Structure**

## Introduction to Arrays

An array is collection of items stored at contiguous memory locations. The idea is to store multiple items of same type together. This makes it easier to calculate the position of each element by simply adding an offset to a base value, i.e., the memory location of the first element of the array (generally denoted by the name of the array).

![array](https://media.geeksforgeeks.org/wp-content/uploads/array-2.png)

⭐ Remember: **Location of next index depends on the data type we use.**

## Types of indexing in array:

- 0（zero-based indexing）: The first element of the array is indexed by subscript of 0
- 1（one-based indexing）: The first element of the array is indexed by subscript of 1
- n （n-based indexing）: The base index of an array can be freely chosen. Usually programming languages allowing n-based indexing also allow negative index values and other scalar data types like enumerations, or characters may be used as an array index.

<img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/Array-In-C.png" alt="img" style="zoom: 67%;" />

## ⭐Advantages of using arrays:

- Arrays allow random access of elements. **This makes accessing elements by position faster.**
- Arrays have better ***[cache locality](https://en.wikipedia.org/wiki/Locality_of_reference)*** that can make a pretty big difference in performance.
- [Cache —— 局部性原理和工作原理](https://blog.csdn.net/starter_____/article/details/97389110)

```cpp
// A character array in C/C++/Java
char arr1[] = {'g', 'e', 'e', 'k', 's'};

// An Integer array in C/C++/Java
int arr2[] = {10, 20, 30, 40, 50};

// Item at i'th index in array is typically accessed
// as "arr[i]".  For example arr1[0] gives us 'g'
// and arr2[3] gives us 40.
```

**Usually, an array of characters is called a 'string'.**

# **Arrays in C/C++**

They can be used to store collection of primitive data types such as int, float, double, char, etc of any particular type. To add to it, an array in C or C++ can store derived data types such as the structures, pointers etc. Given below is the picturesque representation of an array.![arrays](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2015/05/Arrays.png)

## why do we need arrays ?

We can use normal variables (v1, v2, v3, ..) when we have a small number of objects, but if we want to store a large number of instances, it becomes difficult to manage them with normal variables. The idea of an array is to represent many instances in one variable.

## Array <u>declaration</u> in C/C++

<img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/Array-Declaration-In-C.png" alt="img" style="zoom:67%;" />

There are various ways in which we can declare an array. It can be done by specifying its <u>**type**</u> and <u>**size**</u>, by initializing it or both.

1. Array declaration by **<u>specifying size</u>**

   ```cpp
   // Array declaration by specifying size
   int arr1[10];
   
   // With recent C/C++ versions, we can also declare an array of user specified size
   int n = 10;
   int arr2[n];
   ```

2. Array declaration by initializing elements

   ```cpp
   // Array declaration by initializing elements
   int arr[] = {10, 20, 30, 40}
   
   // Compiler creates an array of size 4.
   // above is same as "int arr[4] = {10, 20, 30, 40}"
   ```

3. Array declaration by specifying size and initializing elements

   ```cpp
   // Array declaration by specifying size and initializing 
   // elements 
   int arr[6] = { 10, 20, 30, 40 } 
   
   // Compiler creates an array of size 6, initializes first 
   // 4 elements as specified by user and rest two elements as 0. 
   // above is same as "int arr[] = {10, 20, 30, 40, 0, 0}" 
   
   ```

## Advantages of an Array in C/C++

1. Random access of elements using array index.
2. Use of less line of code as it creates a single array of multiple elements.
3. Easy access to all the elements.
4. Traversal through the array becomes easy using a single loop.
5. Sorting becomes easy as it can be accomplished by writing less line of code.

## Disadvantages of an Array in C/C++

1. Allows a fixed number of elements to be entered which is decided at the time of declaration. Unlike a linked list, an array in C is not dynamic.
2. Insertion and deletion of elements can be costly since the elements are needed to be managed in [accordance](按照，依据；一致，和谐) with the new memory allocation.

## Facts about Array in C/C++

- **Accessing Array Elements:**

- Array elements are accessed by using an integer index. Array index starts wit  and goes till size of array minus 1. See the picture below:![img](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Array-In-C.png)

  **Example:**

  - C

    ```c
    #include <stdio.h> 
    
    int main() 
    { 
    	int arr[5]; 
    	arr[0] = 5; 
    	arr[2] = -10; 
    	arr[3 / 2] = 2; // this is same as arr[1] = 2 
    	arr[3] = arr[0]; 
    
    	printf("%d %d %d %d", arr[0], arr[1], arr[2], arr[3]); 
    
    	return 0; 
    } 
    
    ```

  - C++

    ```cpp
    #include <iostream> 
    using namespace std; 
      
    int main() 
    { 
        int arr[5]; 
        arr[0] = 5; 
        arr[2] = -10; 
      
        // this is same as arr[1] = 2 
        arr[3 / 2] = 2; 
        arr[3] = arr[0]; 
      
        cout << arr[0] << " " << arr[1] 
             << " " << arr[2] << " " << arr[3]; 
      
        return 0; 
    } 
    ```

  - In C, it is not compiler error to initialize an array with more elements than the specified size. For example, the below program compiles fine and shows just Warning.

  - **Note:** The program below won't compile in C++. If we save the above program as a .cpp, the program generates compiler error.

  ```c
  #include <stdio.h> 
  int main() 
  { 
  
  	// Array declaration by initializing it with more 
  	// elements than specified size. 
  	int arr[2] = { 10, 20, 30, 40, 50 }; 
  
  	return 0; 
  } 
  
  ```

  > **Warnings:**
  >
  > ```
  > prog.c: In function 'main':
  > prog.c:7:25: warning: excess elements in array initializer
  >   int arr[2] = { 10, 20, 30, 40, 50 };
  >                          ^
  > prog.c:7:25: note: (near initialization for 'arr')
  > prog.c:7:29: warning: excess elements in array initializer
  >   int arr[2] = { 10, 20, 30, 40, 50 };
  >                              ^
  > prog.c:7:29: note: (near initialization for 'arr')
  > prog.c:7:33: warning: excess elements in array initializer
  >   int arr[2] = { 10, 20, 30, 40, 50 };
  >                                  ^
  > prog.c:7:33: note: (near initialization for 'arr')
  > ```

- The elements are stored at contiguous memory locations

  **Examples:**

  ```c
  // C Language
  // C program to demonstrate that array elements are stored 
  // contiguous locations 
  
  #include <stdio.h> 
  int main() 
  { 
  	// an array of 10 integers. If arr[0] is stored at 
  	// address x, then arr[1] is stored at x + sizeof(int) 
  	// arr[2] is stored at x + sizeof(int) + sizeof(int) 
  	// and so on. 
  	int arr[5], i; 
  
  	printf("Size of integer in this compiler is %lu\n", sizeof(int)); 
  
  	for (i = 0; i < 5; i++) 
  		// The use of '&' before a variable name, yields 
  		// address of variable. 
  		printf("Address arr[%d] is %p\n", i, &arr[i]); 
  
  	return 0; 
  } 
  
  ```

  **Output:**

  ```c
  Size of integer in this compiler is 4
  Address arr[0] is 0x7ffd636b4260
  Address arr[1] is 0x7ffd636b4264
  Address arr[2] is 0x7ffd636b4268
  Address arr[3] is 0x7ffd636b426c
  Address arr[4] is 0x7ffd636b4270
  ```

  ```cpp
  // C++
  // C++ program to demonstrate that array elements 
  // are stored contiguous locations 
  
  #include <iostream> 
  using namespace std; 
  
  int main() 
  { 
  	// an array of 10 integers. If arr[0] is stored at 
  	// address x, then arr[1] is stored at x + sizeof(int) 
  	// arr[2] is stored at x + sizeof(int) + sizeof(int) 
  	// and so on. 
  	int arr[5], i; 
  
  	cout << "Size of integer in this compiler is " << sizeof(int) << "\n"; 
  
  	for (i = 0; i < 5; i++) 
  		// The use of '&' before a variable name, yields 
  		// address of variable. 
  		cout << "Address arr[" << i << "] is " << &arr[i] << "\n"; 
  
  	return 0; 
  } 
  
  ```

  **Output:**

  ```cpp
  Size of integer in this compiler is 4
  Address arr[0] is 0x7ffd636b4260
  Address arr[1] is 0x7ffd636b4264
  Address arr[2] is 0x7ffd636b4268
  Address arr[3] is 0x7ffd636b426c
  Address arr[4] is 0x7ffd636b4270
  ```


## Array vs Pointers

Arrays and pointer are two different things (we can check by applying sizeof). The confusion happens because array name indicates the address of first element and arrays are always passed as pointers(even if we use square bracket)

## What is vector in C++?

Vector in C++ is a class in STL that represents an array. The advantages of vector over normal arrays are,

- We do not need pass size as an extra parameter when we declare a vector i.e, Vectors support **dynamic** **sizes** ( we do not have to initially specify size of a vector ). We can also **resize** a vector.
- Vectors have many in-built function like, adding or removing an element, etc.
- more details of [vector in C++](https://www.geeksforgeeks.org/vector-in-cpp-stl/).

# Initialization of a multidimensional arrays in C/C++

In C/C++, Initialization of a multidimensional arrays can have left most dimension as optional. Except the left most dimension, all other dimensions must be specified.

For example, following program fails in compilation because two dimensions are not specified. 

```cpp
#include<stdio.h> 
int main() 
{ 
int a[][][2] = { {{1, 2}, {3, 4}}, 
				{{5, 6}, {7, 8}} 
				}; // error 
printf("%d", sizeof(a)); 
getchar(); 
return 0; 
} 
```

Following 2 programs work without any error.

```cpp
// Program 1 
#include<stdio.h> 
int main() 
{ 
int a[][2] = {{1,2},{3,4}}; // Works 
printf("%lu", sizeof(a)); // prints 4*sizeof(int) 
getchar(); 
return 0; 
} 

// Program 2 
#include<stdio.h> 
int main() 
{ 
int a[][2][2] = { {{1, 2}, {3, 4}}, 
					{{5, 6}, {7, 8}} 
				}; // Works 
printf("%lu", sizeof(a)); // prints 8*sizeof(int) 
getchar(); 
return 0; 
} 
```



# C# Arrays

In C# the allocation of memory for the arrays is done dynamically. And arrays are kind of objects, therefore it is easy to find their size using the predefined functions. The variables in the array are ordered and each has an index beginning from 0. Arrays in C# differently than they do in C/C++.

**Important Points to Remember About Arrays in C#**

- In C#, all arrays are dynamically allocated.
- Since arrays are objects in C#, we can find their length using member length. This is different from C/C++ where we find length using sizeof operator.
- A C# array variable can also be declared like other variables with [] **after the data type.**
- The variables in the array are ordered and each has an index beginning from 0.
- C# array is an object of base type **System.Array**.
- Default values of numeric array and reference type elements are set to be respectively zero and null.
- A jagged array elements are reference types and are initialized to null.
- Array elements can be of any type, including an array type.
- Array types are reference types which are derived from the abstract base type Array. These types implement **IEnumerable** and for it, they use foreach iteration on all arrays in C#.

The array has can contains primitives data types as well as objects of a  class depending on the definition of an array. Whenever use primitives data types, the actual values have to be stored in contiguous memory locations. In the case of objects of a  class, the actual objects are stored in the heap segment.

The following figure shows how array stores values sequentially :
[![C# Arrays](https://media.geeksforgeeks.org/wp-content/uploads/C-Arrays.jpg)](https://media.geeksforgeeks.org/wp-content/uploads/C-Arrays.jpg)

**Explanation :**
The index is starting from 0, which stores value. we can also store a fixed number of values in an array. Array index is to be increased by 1 in sequence whenever its not reach the array size.

## Array Declaration

As said earlier, an array is a reference type so the new keyword used to create an instance of the **array**. We can assign initialize individual array elements, with the help of the index.

**Syntax:**

```csharp
type [ ] < Name_Array > = new < datatype > [size];
int[] array = new int[10];
```

Here, type specifies the type of data being allocated, size specifies the number of elements in the array, and Name_Array is the name of array variable. And **new** will allocate memory to an array according to its size.

**Examples: To Show Different ways for the Array Declaration and Initialization**

**Example 1 :**

```csharp
// defining array with size 5, but not assigns values
int[] array = new int[5];
```

The above statement declares & initializes int type array that can store five int values. The array size is specified in square brackets([]).

**Example 2 :**

```csharp
// defining array with size 5 and assigning values at the same time
int[] array = new int[5]{1, 2, 3, 4, 5};
```

The above statement is the same as, but it assigns values to each index in {}.

**Example 3 :**

```csharp
// defining array with 5 elements which indicates the size of an array
int[] array = {1, 2, 3, 4, 5};
```

In the above statement, the value of the array is directly initialized without taking its size. So, array size will automatically be the number of values which is directly taken.

## Initialization of an Array after Declaration

Arrays can be initialized after the declaration. It is not necessary to declare and initialize at the same time using the **new** keyword. However, Initializing an Array **after the declaration**, it **<u>must be initialized with the new keyword.</u>** It **can't** be initialized by only assigning values.

**Example :**

```csharp
// Declaration of the array
string[] str1, str2;
// Initialization of array
str1 = new string[5]{ “Element 1”, “Element 2”, “Element 3”, “Element 4”, “Element 5” };

str2 = new string[]{ “Element 1”, “Element 2”, “Element 3”, “Element 4”, “Element 5” };
```

**Note : **Initialization without giving size is not valid in C#. It will give a compile-time error.

**Example : Wrong Declaration for initializing an array**

```csharp
// compile-time error: must give size of an array
int[] intArray = new int[];
// error:wrong initialization of an array
string[] str1;
str1 = {“Element 1”, “Element 2”, “Element 3”, “Element 4” };
```

## Accessing Array Elements

At the time of initialization, we can assign the value. But, we can also assign the value of the array using its index randomly after the declaration and initialization. We can access an array value through indexing, placed index of the element within square brackets with the array name.

**Example : **

```csharp
//declares & initializes int type array
int[] intArray = new int[5];

// assign the value 10 in array on its index 0
intArray[0] = 10; 

// assign the value 30 in array on its index 2
intArray[2] = 30;

// assign the value 20 in array on its index 1
intArray[1] = 20;

// assign the value 50 in array on its index 4
intArray[4] = 50;

// assign the value 40 in array on its index 3
intArray[3] = 40;

// Accessing array elements using index
intArray[0];  //returns 10
intArray[2];  //returns 30
```

**Implementation : Accessing Array elements using different loops**

```csharp
// C# program to illustrate creating an array 
// of integers, puts some values in the array, 
// and prints each value to standard output. 
using System; 
namespace geeksforgeeks { 
	
class GFG { 
	
	// Main Method 
	public static void Main() 
	{ 
		
		// declares an Array of integers. 
		int[] intArray; 

		// allocating memory for 5 integers. 
		intArray = new int[5]; 

		// initialize the first elements 
		// of the array 
		intArray[0] = 10; 

		// initialize the second elements 
		// of the array 
		intArray[1] = 20; 

		// so on... 
		intArray[2] = 30; 
		intArray[3] = 40; 
		intArray[4] = 50; 

		// accessing the elements 
		// using for loop 
		Console.Write("For loop :"); 
		for (int i = 0; i < intArray.Length; i++) 
			Console.Write(" " + intArray[i]); 

		Console.WriteLine(""); 
		Console.Write("For-each loop :"); 
		
		// using for-each loop 
		foreach(int i in intArray) 
			Console.Write(" " + i); 

		Console.WriteLine(""); 
		Console.Write("while loop :"); 
		
		// using while loop 
		int j = 0; 
		while (j < intArray.Length) { 
			Console.Write(" " + intArray[j]); 
			j++; 
		} 

		Console.WriteLine(""); 
		Console.Write("Do-while loop :"); 
		
		// using do-while loop 
		int k = 0; 
		do
		{ 
			Console.Write(" " + intArray[k]); 
			k++; 
		} while (k < intArray.Length); 
	} 
} 
} 

```

## Multidimensional Arrays

The multi-dimensional array contains more than one row to store the values. It is also known as a **Rectangular Array** in C# because it's each row length is same. It can be a **2D-array** or **3D-array** or more. To storing and accessing the values of the array, one required the nested loop. The multi-dimensional array declaration, initialization and accessing is as follows :

```csharp
// creates a two-dimensional array of 
// four rows and two columns.
int[, ] intarray = new int[4, 2];

//creates an array of three dimensions, 4, 2, and 3
int[,, ] intarray1 = new int[4, 2, 3];
```

**Example : **

```csharp
// C# program to illustrate creating 
// an multi- dimensional array 
// puts some values in the array, 
// and print them 
using System; 
namespace geeksforgeeks { 
	
class GFG { 
	
	// Main Method 
	public static void Main() 
	{ 
		
		// Two-dimensional array 
		int[, ] intarray = new int[, ] { { 1, 2 }, 
										{ 3, 4 }, 
										{ 5, 6 }, 
										{ 7, 8 } }; 
										
		// The same array with dimensions 
		// specified 4 row and 2 column. 
		int[, ] intarray_d = new int[4, 2] { { 1, 2 }, { 3, 4 }, 
											{ 5, 6 }, { 7, 8 } }; 

		// A similar array with string elements. 
		string[, ] str = new string[4, 2] { { "one", "two" }, 
											{ "three", "four" }, 
											{ "five", "six" }, 
											{ "seven", "eight" } }; 

		// Three-dimensional array. 
		int[,, ] intarray3D = new int[,, ] { { { 1, 2, 3 }, 
											{ 4, 5, 6 } }, 
											{ { 7, 8, 9 }, 
										{ 10, 11, 12 } } }; 
											
											
		// The same array with dimensions 
		// specified 2, 2 and 3. 
		int[,, ] intarray3Dd = new int[2, 2, 3] { { { 1, 2, 3 }, 
												{ 4, 5, 6 } }, 
												{ { 7, 8, 9 }, 
												{ 10, 11, 12 } } }; 

		// Accessing array elements. 
		Console.WriteLine("2DArray[0][0] : " + intarray[0, 0]); 
		Console.WriteLine("2DArray[0][1] : " + intarray[0, 1]); 
		Console.WriteLine("2DArray[1][1] : " + intarray[1, 1]); 
		Console.WriteLine("2DArray[2][0] " + intarray[2, 0]); 

		Console.WriteLine("2DArray[1][1] (other) : "
								+ intarray_d[1, 1]); 
								
		Console.WriteLine("2DArray[1][0] (other)"
							+ intarray_d[1, 0]); 

		Console.WriteLine("3DArray[1][0][1] : "
						+ intarray3D[1, 0, 1]); 
							
		Console.WriteLine("3DArray[1][1][2] : "
						+ intarray3D[1, 1, 2]); 

		Console.WriteLine("3DArray[0][1][1] (other): "
							+ intarray3Dd[0, 1, 1]); 
							
		Console.WriteLine("3DArray[1][0][2] (other): "
							+ intarray3Dd[1, 0, 2]); 

		// using nested loop show string elements 
		Console.WriteLine("To String element"); 
		for (int i = 0; i < 4; i++) 
			for (int j = 0; j < 2; j++) 
				Console.Write(str[i, j] + " "); 
	} 
} 
} 

```
