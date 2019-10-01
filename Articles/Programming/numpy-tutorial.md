NumPy Tutorial: A Simple Example-Based Guide
===

-   [Introduction](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#introduction)
-   [Advantages of NumPy](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#advantagesofnumpy)
-   [NumPy Operations](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#numpyoperations)
-   [Creating a NumPy Array](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#creatinganumpyarray)
    -   [The array Method](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#thearraymethod)
    -   [The arange Method](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#thearangemethod)
    -   [The zeros Method](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#thezerosmethod)
    -   [The ones Method](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#theonesmethod)
    -   [The linspace Method](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#thelinspacemethod)
    -   [The eye Method](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#theeyemethod)
    -   [The random Method](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#therandommethod)
-   [Reshaping NumPy Array](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#reshapingnumpyarray)
-   [Finding Max/Min Values](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#findingmaxminvalues)
-   [Array Indexing in NumPy](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#arrayindexinginnumpy)
    -   [Indexing with 1-D Arrays](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#indexingwith1darrays)
    -   [Indexing with 2-D Arrays](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#indexingwith2darrays)
-   [Arithmetic Operations with NumPy Arrays](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#arithmeticoperationswithnumpyarrays)
    -   [The log Function](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#thelogfunction)
    -   [The exp Function](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#theexpfunction)
    -   [The sqrt Function](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#thesqrtfunction)
    -   [The sin Function](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#thesinfunction)
-   [Linear Algebra Operations with NumPy Arrays](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#linearalgebraoperationswithnumpyarrays)
    -   [Finding the Vector Dot Product](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#findingthevectordotproduct)
    -   [Matrix Multiplication](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#matrixmultiplication)
    -   [Finding the Inverse of a Matrix](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#findingtheinverseofamatrix)
    -   [Finding the Determinant of a Matrix](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#findingthedeterminantofamatrix)
    -   [Finding the Trace of a Matrix](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#findingthetraceofamatrix)
-   [Conclusion](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/#conclusion)

### Introduction

The  [NumPy](https://www.numpy.org/)  library is a popular Python library used for scientific computing applications, and is an acronym for "Numerical Python". NumPy's operations are divided into three main categories:  [Fourier Transform](https://en.wikipedia.org/wiki/Fourier_transform)  and Shape Manipulation, Mathematical and Logical Operations, and Linear Algebra and Random Number Generation. To make it as fast as possible, NumPy is written in C and Python.

In this article, we will provide a brief introduction to the NumPy stack and we will see how the NumPy library can be used to perform a variety of mathematical tasks.

### Advantages of NumPy

NumPy has several advantages over using core Python mathemtatical functions, a few of which are outlined here:

1.  NumPy is extremely fast when compared to core Python thanks to its heavy use of C extensions.
2.  Many advanced Python libraries, such as Scikit-Learn, Scipy, and Keras, make extensive use of the NumPy library. Therefore, if you plan to pursue a career in data science or machine learning, NumPy is a very good tool to master.
3.  NumPy comes with a variety of built-in functionalities, which in core Python would take a fair bit of custom code.

Regarding the last point, take a look at the following script:

```python
x = [2, 3, 4, 5, 6]
y = [a + 2 for a in x]

```

Here, in order to add 2 to each element in the list  `x`, we have to traverse the entire list and add 2 to each element individually. Now let's see how we can perform the same task with the NumPy library:

```python
import numpy as np
nums = np.array([2, 3, 4, 5, 6])
nums2 = nums + 2

```

You can see how easy it is to add a scalar value to each element in the list via NumPy. It is not only readable, but also faster when compared to the previous code.

This is just the tip of the iceberg, in reality, the NumPy library is capable of performing far more complex operations in the blink of an eye. Let's explore some of these operations.

### NumPy Operations

Before we can perform any NumPy operations, we need to install the NumPy package. To install the NumPy package, you can use the pip installer. Execute the following command to install:

```sh
$ pip install numpy

```

Otherwise, if you are running Python via the Anaconda distribution, you can execute the following command instead:

```sh
$ conda install numpy

```

Now that NumPy is installed, let's see some of the most common operations of the library.

#### Creating a NumPy Array

NumPy arrays are the building blocks of most of the NumPy operations. The NumPy arrays can be divided into two types: One-dimensional arrays and Two-Dimensional arrays.

There are several ways to create a NumPy array. In this section, we will discuss a few of them.

##### The array Method

To create a one-dimensional NumPy array, we can simply pass a Python list to the  `array`  method. Check out the following script for an example:

```python
import numpy as np
x = [2, 3, 4, 5, 6]
nums = np.array([2, 3, 4, 5, 6])
type(nums)

```

In the script above we first imported the NumPy library as  `np`, and created a list  `x`. We then passed this list to the  `array`  function of the NumPy library. Finally, we printed the type of the array, which resulted in the following output:

```
numpy.ndarray

```

If you were to print the  `nums`  array on screen, you would see it displayed like this:

```
array([2, 3, 4, 5, 6])

```

To create a two-dimensional array, you can pass a list of lists to the  `array`  method as shown below:

```python
nums = np.array([[2,4,6], [8,10,12], [14,16,18]])

```

The above script results in a matrix where every inner list in the outer list becomes a row. The number of columns is equal to the number of elements in each inner list. The output matrix will look like this:

```
array([[ 2,  4,  6],
       [ 8, 10, 12],
       [14, 16, 18]])

```

##### The arange Method

Another commonly used method for creating a NumPy array is the  `arange`  method. This method takes the start index of the array, the end index, and the step size (which is optional). Take a look at the following example:

```python
nums = np.arange(2, 7)

```

Simple enough, right? The above script will return a NumPy array of size 5 with the elements 2, 3, 4, 5, and 6. Remember that the  `arange`  method returns an array that starts with the starting index and ends at one index less than the end index. The output of this code looks like this:

```
array([2, 3, 4, 5, 6])

```

Now let's add a step size of 2 to our array and see what happens:

```python
nums = np.arange(2, 7, 2)

```

The output now looks like this:

```
array([2, 4, 6])

```

You can see that array starts at 2, followed by a step size of 2 and ends at 6, which is one less than the end index.

##### The zeros Method

Apart from generating custom arrays with your pre-filled data, you can also create NumPy arrays with a simpler set of data. For instance, you can use the  `zeros`  method to create an array of all zeros as shown below:

```python
zeros = np.zeros(5)

```

The above script will return a one-dimensional array of 5 zeros. Print the  `zeros`  array and you should see the following:

```
array([0., 0., 0., 0., 0.])

```

Similarly, to create a two-dimensional array, you can pass both the number of rows and columns to the  `zeros`  method, as shown below:

```python
zeros = np.zeros((5, 4))

```

The above script will return a two-dimensional array of 5 rows and 4 columns:

```
array([[0., 0., 0., 0.],
       [0., 0., 0., 0.],
       [0., 0., 0., 0.],
       [0., 0., 0., 0.],
       [0., 0., 0., 0.]])

```

##### The ones Method

Similarly, you can create one-dimensional and two-dimensional arrays of all ones using the  `ones`  method as follows:

```python
ones = np.ones(5)

```

```
array([1., 1., 1., 1., 1.])

```

And again, for the two-dimensional array, try out the following code:

```python
ones = np.ones((5, 4))

```

Now if you print the  `ones`  array on the screen, you should see the following two-dimensional array:

```
[[1. 1. 1. 1.]
 [1. 1. 1. 1.]
 [1. 1. 1. 1.]
 [1. 1. 1. 1.]
 [1. 1. 1. 1.]]

```

##### The linspace Method

Another very useful method to create NumPy arrays is the  `linspace`  method. This method takes three arguments: a start index, end index, and the number of linearly-spaced numbers that you want between the specified range. For instance, if the first index is 1, the last index is 10 and you need 10 equally spaced elements within this range, you can use the  `linspace`  method as follows:

```python
lin = np.linspace(1, 10, 10)

```

The output will return integers from 1 to 10:

```
array([1., 2., 3., 4., 5., 6., 7., 8., 9., 10.])

```

Now let's try to create an array with 20 linearly-spaced elements between 1 and 10. Execute the following script:

```python
lin = np.linspace(1, 10, 20)

```

This will result in the following array:

```
array([ 1.        ,  1.47368421,  1.94736842,  2.42105263,  2.89473684,
        3.36842105,  3.84210526,  4.31578947,  4.78947368,  5.26315789,
        5.73684211,  6.21052632,  6.68421053,  7.15789474,  7.63157895,
        8.10526316,  8.57894737,  9.05263158,  9.52631579, 10.        ])

```

Notice that the output might look like a matrix, but actually it is a one-dimensional array. Because of the spacing issue, the elements have been displayed in multiple lines.

##### The eye Method

The  `eye`  method can be used to create an  [identity matrix](https://en.wikipedia.org/wiki/Identity_matrix), which can be very useful to perform a variety of operations in linear algebra. An identity matrix is a matrix with zeros across rows and columns except the diagonal. The diagonal values are all ones. Let's create a 4x4 identity matrix using the  `eye`  method:

```python
idn = np.eye(4)

```

The resultant matrix looks like this:

```
array([[1., 0., 0., 0.],
       [0., 1., 0., 0.],
       [0., 0., 1., 0.],
       [0., 0., 0., 1.]])

```

##### The random Method

Often times you will need to create arrays with random numbers. You can use the  `rand`  function of NumPy's  `random`  module to do so. Here is a simple example of the  `rand`  function:

```python
random = np.random.rand(2, 3)

```

The above script returns a matrix of 2 rows and 3 columns. The matrix contains uniform distribution of numbers between 0 and 1:

```
array([[0.26818562, 0.65506793, 0.50035001],
       [0.527117  , 0.445688  , 0.99661   ]])

```

Similarly, to create a matrix of random numbers with the  [Gaussian distribution](https://en.wikipedia.org/wiki/Normal_distribution)  (or "normal" distribution), you can instead use the  `randn`  method as shown below:

```python
random = np.random.randn(2, 3)

```

Finally, to create an array of random integers, the  `randint`  method exists for such a case. The  `randint`  method takes the lower bound, upper bound, and the number of integers to return. For instance, if you want to create an array of 5 random integers between 50 and 100, you can use this method as follows:

```python
random = np.random.randint(50, 100, 5)

```

In our case, the output looked like this:

```
array([54, 59, 84, 62, 74])

```

It is important to mention that these numbers are generated randomly every time you call the method, so you will see different numbers than in our example.

We saw different ways of creating Python arrays. Let's now explore some of the other array functions.

#### Reshaping NumPy Array

Using NumPy you can convert a one-dimensional array into a two-dimensional array using the  `reshape`  method.

Let's first create an array of 16 elements using the  `arange`  function. Execute the following code:

```python
nums = np.arange(1, 17)

```

The  `nums`  array is a one-dimensional array of 16 elements, ranging from 1 to 16:

```
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16])

```

Nos let's convert it into a two-dimensional array of 4 rows and 4 columns:

```python
nums2 = nums.reshape(4, 4)

```

The array now looks like this:

```
array([[ 1,  2,  3,  4],
       [ 5,  6,  7,  8],
       [ 9, 10, 11, 12],
       [13, 14, 15, 16]])

```

It is pertinent to mention that you cannot reshape an array if the number of elements in the one-dimensional array is not equal to the product of rows and columns of the reshaped array. For instance, if you have 45 elements in a 1-d array, you cannot reshape it into a matrix of 5 row and 10 columns since a 5x10 matrix has 50 elements and the original one only has 45.

#### Finding Max/Min Values

You can use  `min`/`max`  functions to easily find the value of the smallest and largest number in your array. For our example, let's first create an array of 5 random integers:

```python
random = np.random.randint(1, 100, 5)
print(random)

```

Our array of random integers looks like this:

```
[51 40 84 38  1]

```

Remember, these numbers are generated randomly, therefore you will most likely have a different set of numbers. Let's use  `min`  and  `max`  functions to find the minimum and maxim values from the array that we just created. To do so, execute the following code to find minimum value:

```python
xmin = random.min()
print(xmin)

```

"1" will be printed in the output.

Similarly, for maximum value, execute the following code:

```python
xmax = random.max()
print(xmax)

```

The above script will return "84" as the output.

You can also find the  _index_  of the maximum and minimum values using the  `argmax()`  and  `argmin()`  functions. Take a look at the following script:

```python
print(random.argmax())

```

The above script will print "2" since 84 is the largest number in the list and it is located at the second position of the array.

Similarly, the  `argmin()`  will return "4" because 1 is the smallest number and is located at the 4th position.

#### Array Indexing in NumPy

In order to effectively use the NumPy arrays, it is very important to understand the way the arrays are indexed, which I'll discuss in the next few sections.

##### Indexing with 1-D Arrays

Let's create a simple array of 15 numbers:

```python
nums = np.arange(1, 16)

```

You can retrieve any element by passing the index number. Just like Python's lists, NumPy's arrays are zero-indexed. For instance, to find the element at the second index (3rd position) of the array, you can use the following syntax:

```python
print(nums[2])

```

We have the digit 3 at the second index, therefore it will be printed on the screen.

#### Subscribe to our Newsletter

Get occassional tutorials, guides, and reviews in your inbox. No spam ever. Unsubscribe at any time.

Subscribe

You can also print a range of numbers using indexing. To get the range, you need to pass the start index and one less than the end index, separated by a colon, inside the square brackets that follow the array name. For example, to get the elements from the first to seventh index, you can use the following syntax:

```python
print(nums[1:8])

```

The above script will print the integers from 2 to 8:

```
[2 3 4 5 6 7 8]

```

Here in the  `nums`  array, we have 2 at index 1 and 8 at index seven.

You can also slice an array and assign the elements of the sliced array to a new array:

```python
nums2 = nums[0:8]
print(nums2)

```

In the script above we sliced the  `nums`  array by extracting its first 8 elements. The resultant elements are assigned to the  `nums2`  array. We then print the  `nums2`  array to the console. The output is a new array of the first 8 numbers:

```
[1 2 3 4 5 6 7 8]

```

##### Indexing with 2-D Arrays

Indexing a two-dimensional NumPy array is very similar to indexing a matrix. Let's first create 3x3 two-dimensional NumPy array. To do so, run the following code:

```python
nums2d = np.array(([1,2,3],[4,5,6],[7,8,9]))

```

Now let's print it out:

```python
print(nums2d)

```

```
[[1 2 3]
 [4 5 6]
 [7 8 9]]

```

Like 1-D arrays, NumPy arrays with two dimensions also follow the zero-based index, that is, in order to access the elements in the  _first_  row, you have to specify 0 as the row index. Similarly to access elements in the first column, you need to specify 0 for the column index as well.

Let's retrieve an element from  `nums2d`  array, located in the first row and first column:

```python
print(nums2d[0, 0])

```

You will see "1" in the output. Similarly, we can retrieve the element at the third row and third column as follows:

```python
print(nums2d[2, 2])

```

You will see "9" in the output.

In addition to extracting a single element, you can extract the whole row by passing only the row index to the square brackets. For instance, the following script returns the first row from the  `nums2d`  array:

```python
print(nums2d[0])

```

The output just a one-dimensional array:

```
[1 2 3]

```

Similarly to retrieve the first column only, you can use the following syntax:

```python
print(nums2d[:,0])

```

The output is, again, an array, but it is a combination of the first elements of each array of the two-dimensional array:

```
[1 4 7]

```

Finally, to retrieve the elements from the first two rows and first two columns, the following syntax can be used:

```python
print(nums2d[:2,:2])

```

The above script returns the following output:

```
[[1 2]
 [4 5]]

```

#### Arithmetic Operations with NumPy Arrays

For the examples in this section, we will use the  `nums`  array that we created in the last section.

Let's first add two arrays together:

```python
nums3 = nums + nums

```

You can add two arrays together with the same dimensions. For instance, the  `nums`  array contained 15 elements, therefore we can add it to itself. The elements at the corresponding indexes will be added. Now if you print the  `nums3`  array, the output looks like this:

```
[ 2  4  6  8 10 12 14 16 18 20 22 24 26 28 30]

```

As you can see, each position is the sum of the 2 elements at that position in the original arrays.

If you add an array with a scalar value, the value will be added to  _each element_  in the array. Let's add 10 to the  `nums`  array and print the resultant array on the console. Here is how you'd do it:

```python
nums3 = nums + 10
print(nums3)

```

And the resulting  `nums3`  array becomes:

```
[11 12 13 14 15 16 17 18 19 20 21 22 23 24 25]

```

Subtraction, addition, multiplication, and division can be performed in the same way.

Apart from simple arithmetic, you can execute more complex functions on the Numpy arrays, e.g. log, square root, exponential, etc.

##### The log Function

The following code simply returns an array with the log of all elements in the input array:

```python
nums3 = np.log(nums)
print(nums3)

```

The output looks like this:

```
[0.         0.69314718 1.09861229 1.38629436 1.60943791 1.79175947
 1.94591015 2.07944154 2.19722458 2.30258509 2.39789527 2.48490665
 2.56494936 2.63905733 2.7080502 ]

```

##### The exp Function

The following script returns an array with exponents of all elements in the input array:

```python
nums3 = np.exp(nums)
print(nums3)

```

```
[2.71828183e+00 7.38905610e+00 2.00855369e+01 5.45981500e+01
 1.48413159e+02 4.03428793e+02 1.09663316e+03 2.98095799e+03
 8.10308393e+03 2.20264658e+04 5.98741417e+04 1.62754791e+05
 4.42413392e+05 1.20260428e+06 3.26901737e+06]

```

##### The sqrt Function

The following script returns an array with the square roots of all the elements in the input array:

```python
nums3 = np.sqrt(nums)
print(nums3)

```

```
[1.         1.41421356 1.73205081 2.         2.23606798 2.44948974
 2.64575131 2.82842712 3.         3.16227766 3.31662479 3.46410162
 3.60555128 3.74165739 3.87298335]

```

##### The sin Function

The following script returns an array with the sine of all the elements in the input array:

```python
nums3 = np.sin(nums)
print(nums3)

```

```
[ 0.84147098  0.90929743  0.14112001 -0.7568025  -0.95892427 -0.2794155
  0.6569866   0.98935825  0.41211849 -0.54402111 -0.99999021 -0.53657292
  0.42016704  0.99060736  0.65028784]

```

#### Linear Algebra Operations with NumPy Arrays

One of the biggest advantages of the NumPy arrays is their ability to perform linear algebra operations, such as the vector dot product and the matrix dot product, much faster than you can with the default Python lists.

##### Finding the Vector Dot Product

Computing the vector  [dot product](https://en.wikipedia.org/wiki/Dot_product)  for the two vectors can be calculated by multiplying the corresponding elements of the two vectors and then adding the results from the products.

Let's create two vectors and try to find their dot product manually. A vector in NumPy is basically just a 1-dimensional array. Execute the following script to create our vectors:

```python
x = np.array([2,4])
y = np.array([1,3])

```

The dot product of the above two vectors is  `(2 x 1) + (4 x 3) = 14`.

Let's find the dot product without using the NumPy library. Execute the following script to do so:

```python
dot_product = 0
for a,b in zip(x,y):
    dot_product += a * b

print(dot_product)

```

In the script above, we simply looped through corresponding elements in  `x`  and  `y`  vectors, multiplied them and added them to the previous sum. If you run the script above, you will see "14" printed to the console.

Now, let's see how we can find the dot product using the NumPy library. Look at the following script:

```python
a = x * y
print(a.sum())

```

We know that if we multiply the two NumPy arrays, the corresponding elements from both arrays are multiplied based on their index. In the script above, we simply multiplied the  `x`  and  `y`  vectors. We then call the  `sum`  method on the resultant array, which sums all the elements of the array. The above script will also return "14" in the output.

The above method is simple, however, the NumPy library makes it even easier to find the dot product via the  `dot`  method, as shown here:

```python
print(x.dot(y))

```

For very large arrays you should also notice a speed improvement over our Python-only version, thanks to NumPy's use of C code to implement many of its core functions and data structures.

##### Matrix Multiplication

Like the dot product of two vectors, you can also multiply two matrices. In NumPy, a matrix is nothing more than a two-dimensional array. In order to multiply two matrices, the inner dimensions of the matrices must match, which means that the number of columns of the matrix on the left should be equal to the number of rows of the matrix on the right side of the product. For instance, if a matrix X has dimensions [3,4] and another matrix Y has dimensions of [4,2], then the matrices X and Y can be multiplied together. The resultant matrix will have the dimensions [3,2], which is the size of the outer dimensions.

To multiply two matrices, the  `dot`  function can be used as shown below:

```python
X = np.array(([1,2,3], [4,5,6]))

Y = np.array(([1,2], [4,5], [7,8]))

Z = np.dot(X, Y)

print(Z)

```

In the script above we created a 3x2 matrix named  `X`  and a 2x3 matrix named  `Y`. We then find the dot product of the two matrices and assigned the resultant matrix to the variable  `Z`. Finally, we print the resultant matrix to the console. In the output you should see a 2x2 matrix as shown below:

```
[[30 36]
 [66 81]]

```

You can also multiply the two matrices element-wise. To do so, the dimensions of the two matrices must match, just like when we were adding arrays together. The  `multiply`  function is used for element-wise multiplication.

Let's try to multiply the matrices  `X`  and  `Y`  element-wise:

```python
Z = np.multiply(X, Y)

```

The following error will occur when you run the above code:

```
ValueError: operands could not be broadcast together with shapes (2,3) (3,2)

```

The error occurs due to the mismatch between the dimensions of the  `X`  and  `Y`  matrices. Now, let's try multiplying the  `X`  matrix with itself using the  `multiply`  function:

```python
Z = np.multiply(X, X)

```

Now if you print the  `Z`  matrix, you should see the following result:

```
[[ 1  4  9]
 [16 25 36]]

```

The  `X`  matrix was successfully able to multiple with itself because the dimensions of the multiplied matrices matched.

##### Finding the Inverse of a Matrix

Another very useful matrix operation is finding the inverse of a matrix. The NumPy library contains the  `ìnv`  function in the  `linalg`  module.

For our example, let's find the inverse of a 2x2 matrix. Take a look at the following code:

```python
Y = np.array(([1,2], [3,4]))
Z = np.linalg.inv(Y)
print(Z)

```

The output of the above code looks like this:

```
[[-2.   1. ]
 [ 1.5 -0.5]]

```

Now in order to verify if the inverse has been calculated correctly, we can take the dot product of a matrix with its inverse, which should yield an identity matrix.

```python
W = Y.dot(Z)
print(W)

```

```
[[1.00000000e+00 1.11022302e-16]
 [0.00000000e+00 1.00000000e+00]]

```

And the result was as we expected. Ones in the diagonal and zeros (or very close to zero) elsewhere.

##### Finding the Determinant of a Matrix

The  [determinant](https://en.wikipedia.org/wiki/Determinant)  of a matrix can be calculated using the  `det`  method, which is shown here:

```python
X = np.array(([1,2,3], [4,5,6], [7,8,9]))

Z = np.linalg.det(X)

print(Z)

```

In the script above, we created a 3x3 matrix and found its determinant using the  `det`  method. In the output, you should see "6.66133814775094e-16".

##### Finding the Trace of a Matrix

The trace of a matrix is the sum of all the elements in the diagonal of a matrix. The NumPy library contains  `trace`  function that can be used to find the trace of a matrix. Look at the following example:

```python
X = np.array(([1,2,3], [4,5,6], [7,8,9]))

Z = np.trace(X)

print(Z)

```

In the output, you should see "15", since the sum of the diagonal elements of the matrix  `X`  is  `1 + 5 + 9 = 15`.

### Conclusion

Pythons NumPy library is one of the most popular libraries for numerical computing. In this article, we explored the NumPy library in detail with the help of several examples. We also showed how to perform different linear algebra operations via the NumPy library, which are commonly used in many data science applications.

While we covered quite a bit of NumPy's core functionality, there is still a lot to learn. If you want to learn more, I'd suggest you try out a course like  [Data Science in Python, Pandas, Scikit-learn, Numpy, Matplotlib](https://stackabu.se/data-science-python-pandas-sklearn-numpy), which covers NumPy, Pandas, Scikit-learn, and Matplotlib in much more depth than what we were able to cover here.

I would suggest you practice the examples in this article. If you are planning to start a career as a data scientist, the NumPy library is definitely one of the tools that you must need to learn to be a successful and productive member of the field.

Reference : [https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/](https://stackabuse.com/numpy-tutorial-a-simple-example-based-guide/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA2NTg0MzYzMl19
-->