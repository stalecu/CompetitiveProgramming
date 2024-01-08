# Arrays
## What are they?
Arrays are defined as being a collection of _elements_ (which can be either constant values or variables) _of same memory 
size_, each identified by an _index_. Think of an array like a row of flowers in your garden, all with a certain "index"
("the first flower", "the second flower" etc.). You can also imagine them like an apartment, because they're fixed in size,
and the index could be the apartment number.

Arrays are characterized by the following properties:
- **Homogeneous Elements**: All elements in an array must be of the same data type, meaning they have the same memory size
(for example, an array of integers or an array of characters or an array of flowers); 
- **Contiguous Memory Storage**: Array elements are stored in adjacent memory locations. This contiguous storage allows 
for efficient access and manipulation of elements.
- **Sequential Order**: The elements in an array follow a specific order. Each element is accessed using its index, 
starting from the first element (index 0) to the last element. 
  > 📝 **Note**: Not all programming languages start indexing at zero (also called zero-indexed languages). There
  > are languages that start their indexing at one (one-indexed languages), and even _n_-indexed languages in rare cases.
  > There are valid reasons to choose either 0-indexing or 1-indexing, but your programming language will most likely 
  > prove to be a decisive factor when choosing either indexing scheme. 1-indexing is more natural for us (you don't 
  > usually count from 0), but 0-indexing is more efficient for the machine for reasons I'll touch on later. 

## Why do we need them?
There are plenty of times when we need to store multiple related things (for example, a school record book where you have
a list of students along with their names and grades for each subjects, or multiple elements that you need to filter). 
Arrays are also good because you can instantly retrieve elements from an array, given its index. Sorting and searching in
an array is simpler and easier. 

## Types of arrays
### Static arrays
The simplest type of array is the static array (which is more commonly referred to as just an array, sometimes 
incorrectly a "list" or a "vector"). These are just like the aforementioned row of flowers. Here's how that would look
like in C++:

```cpp
int arr[5] = { 1, 4, 8, 3, 9 };
// arr[0] = 1
// arr[1] = 4
// arr[2] = 8
// arr[3] = 3
// arr[4] = 9

// arr[5] gives an error, since you're going over the boundaries
// of the array. Be careful!
```
C++ is a zero-index language, so the first element is located at `array[0]`, the second at `array[1]` and the last at 
`array[4]`. Alternatively, there is a better way to do it using C++ standard library (you need to include `<array>` for
this):
```cpp
std::array<int, 5> arr { 1, 4, 8, 3, 9 };
```
Same indexing rules apply, except that `std::array` has way more convenient functions and is more powerful than the 
regular C-style array syntax.
> 📝 **Note**: With the C-style syntax, you can actually omit the size and let the compiler figure out the size. Because it
> needs to determine the size from the elements, you have to define the array in the same place where you declare it:
> ```cpp
> int a[] = { 1, 2, 3, 4 };
> // The compiler figured out that the type should actually
> // be int[4] (so 4 integers).
> ```
> Additionally, if your compiler supports C++17 and later, you can achieve a similar thing using C++ deduction guides:
> ```cpp
> std::array arr { 1, 2, 3, 4 };
> // It deduces that arr should be of type std::array<int, 4>
> ```

You can calculate an element's offset in one such array based on the base address of the array + the size of the element.
More specifically, for a general array, $a_i = B + c \cdot i$, where $B$ is the base address of the array, and $c$ is the
size of the type (sometimes called a _stride_ or _address increment_). This is why a lot of programming languages choose
0-indexing: if $i = 0$, then the address of the first element becomes the base address. As a consequence, this also means
that, in order to have $N$ elements, the last index has to be $N - 1$. It's something to keep in mind, since this can and
_will_ trip you up, being a common enough source of errors to have its own name: “off-by-one errors”.

## Dynamic arrays
While static arrays have a fixed size that is determined at compile time (the $N$ in `T a[N]` or `std::array<T, N>`) so
it knows how much memory to allocate, sometimes we don't know that. For that, dynamic arrays, such as `std::vector` in
the STL (Standard Template Library, where `std::array` is also located), allow for... well, dynamic resizing, which makes
them very versatile. It automatically handles resizing and memory management. The same semantics of an array apply to
`std::vector`, but we also have methods to change the size of a vector at runtime (adding elements, removing them or 
resizing the entire vector, among other ways). You need to import it from `<vector>`.

Here is how you would initialize such a vector:
```cpp
std::vector<int> v1 {2, 7, 9}; // v1[0] = 2, v1[1] = 7, v1[2] = 9
std::vector<long> v2 {5, 2};   // v2[0] = 5, v2[1] = 2
```
If you need it to have $N$ elements, you can pass that into its constructor:
```cpp
std::vector<int> v3(10);
```
> 📝 **Note**: `v3` has 10 elements initialized with whatever the default value is for that particular type (in our case, 
> it's 0, but for `bool` it's `false`, for a string it's the empty string etc.)

You can also initialize these $N$ elements using a value, like this:
```cpp
std::vector<int> v4(5, 2);
```
where `v4` now has 5 elements initialized with 2.
> ⚠️ **Warning**: The distinction between `{}` and `()` is crucial here! 
> ```c++
> std::vector<char> A {5, 2};
> std::vector<char> B (5, 2);
> ```
> `A` contains _just_ the elements 5 and 2, while B contains 2, 2, 2, 2, 2 (5 elements that are 2). 

## Multidimensional arrays
A multidimensional array is an array with more than one level or dimension. If we use our row of flowers analogy, then a
two-dimensional (or 2D) array would be a nice little cute garden. :) It is essentially a matrix of rows and columns, like
a table. You can also have three-dimensional (3D) arrays and so on. 

A two-dimensional array is, strictly speaking, an array of arrays, a three-dimensional is an array of two-dimensional 
arrays (think like how a cube is a three-dimensional object, but you can describe it by its faces which are two-dimensional
things), or an array of arrays of arrays. 

Here is how you'd express a two-dimensional _static_ array using both the C-style way and the STL `std::array`:
```cpp
int garden[3][5];
std::array<std::array<int, 5>, 3> garden2;
```
The `std::array` really emphasizes the array of arrays aspect. These have three rows and five columns. You can read the 
last statement from outside to inside: you have an array that contains 3 rows, and each row has 5 elements (or columns 
in the context of this garden). 

The C-style says the same thing but in a different fashion. Let's suppose we have a type named `Row` that is an array of
five elements:
```cpp
using Row = int[5];
```
so a row contains five elements (or columns). We can thus express `garden` as:
```cpp
Row garden[3];
```
or
```cpp
using Row = int[5];
using Garden = Row[3];
```
or 3 rows of 5 elements each! Actually, you can do the same for `std::array`:
```cpp
using Row = std::array<int, 5>;
using Garden = std::array<Row, 3>;
```

With a dynamic array such as `std::vector`, we also have the same array of arrays logic:
```cpp
std::vector<std::vector<int>> table;
```

Unlike its static counterparts, the number of rows and columns is undetermined. It can also let us create _jagged_ arrays,
which are arrays of arrays of which the member arrays can be of different lengths. They are thus not strictly rectangular.
> 📝 **Note**: It doesn't mean you _can't_ do jagged arrays using C-style arrays, but you're dealing with pointers and 
> it's a pain.

If we need the table to have a fixed size (or rather, a starting size), let's say $M \times N$, we can do this:
```cpp
const int M = 3, N = 4;
std::vector<std::vector<int>> table(M, std::vector<int>(N, 0));
```
We can also use `using` statements to unclutter this:
```cpp 
using Row = std::vector<int>;
using Table = std::vector<Row>;

const int M = 3, N = 4;
Table table(M, Row(N, 0));
```
This uses the initialization we've learned for `std::vector`. Instead of initializing it with a single value, we're 
initializing the table with $M$ `Row`s of $N$ elements filled with zeros.

Initializing such arrays is the same as in the one-dimensional case:
```cpp 
int x[4][2] {
      {1, 2},
      {3, 4},
      {5, 6},
      {7, 8}
};

std::array<std::array<int, 5>, 3> y {{
    {1, 2, 3, 4, 5}, 
    {0, 0, 0, 5, 5}, 
    {0, 0, 0, 1, 1}
}};

std::vector<std::vector<int>> z {{
    {1, 0, 4}, 
    {0, 1, 0, 7, 9}, 
    {0}
}};
```
> ⚠️ **Warning**: Notice the single `{}` in the C-style 2D array case vs. the double `{{}}` in the STL elements. The
> explanation is a bit technical, and honestly it doesn't matter for the purposes of using this, and the compiler or
> the editor will tell you that it's wrong anyway.

> 📝 **Note**: `z` is an example of a jagged array. It doesn't need to know the exact dimensions of the data that will
> be contained within, it can determine that automatically. 

When in doubt, use `std::vector`, unless you have a good reason not to (such as when you absolutely need to have a fixed
amount of memory, although you can do the same with a vector too).

Indexing works in a similar fashion to the one-dimensional case:
```cpp 
x[1][3] = 4;
y[3][1] = -1;
z[3][0] = 10;
```

Obviously, this scales to the general N-dimensional case. 

> 📝 **Note**: If you have a two-dimensional static array (or dynamic arrays, as long as you don't have jagged arrays),
> you obviously have $M \times N$ elements, so these:
> ```cpp
> std::array<std::array<int, 5>, 3> A;
> std::array<int, 15> B;
> ```
> are equivalent when it comes to how they're stored in memory. Thus, one might assume that you should be able to find
> a way to index into `B` like how you'd index into `A`, and that's right. The formula is $i \cdot N + j$, where $N$ is 
> the number of columns. The intuition behind that is that $i \cdot N$ brings you to `B[i][0]` and thus $i \cdot N + j$ 
> is `B[i][j]`. In our particular case:
> ```cpp
> B[i * 5 + j] == A[i][j]
> ```
> And we could copy the data from `A` to `B` like this:
> ```cpp
> const int M = 3, N = 5;
> 
> for (std::size_t i = 0; i < M; ++i) {
>     for (std::size_t j = 0; j < N; ++j) {
>         B[i * N + j] = A[i][j]; 
>     }
> }
> ```

Now, let's see some common operations you'd want to do with these arrays.
## Operations on arrays and vectors

I already presented indexing in the previous section, so I won't go into that aspect. 

An important thing we would want to do is iterating over the elements of an array. For that, let's see how to find the
size.

For C-style arrays, we don't have a nice way of doing this using C++, so we're resorting to more primitive ways. 
> ⚠️ **Warning**: This method will only work for standalone arrays, not for arrays passed as function arguments. The
> reason is that when you're doing this approach, it will only give the size of the pointer and not the intended size.
> This can be mitigated by adding another level of pointer and use `sizeof *result`, or by just keeping track of those.
> Unless you don't know the number of elements in each direction, you can't do much. Also, the compiler treats `int[3]`
> and `int*` as different types, even though the former can be decayed to the latter. The main takeaway: it's a huge pain.

```cpp
// This is for a simple 1D array:
short arr[5] = {3, 4, 5, 0, 1};
std::size_t M, N; 

N = sizeof(arr) / sizeof(*arr); 
// ^ You can also use arr[0] instead of *arr.

std::cout << "arr has " << N << " elements\n";

// And for the 2D case:
int mat[3][4] = {{0, 1,  2,  3}, 
                 {4, 5,  6,  7}, 
                 {8, 9, 10, 11}};

M = sizeof(mat) / sizeof(mat[0]);
N = sizeof(mat[0]) / sizeof(mat[0][0]);

std::cout << "mat has " << M << "x" << N << " elements\n";
```

On the STL side though, this is so much simpler, since you have a method for that: `size()`. We'll not deal with jagged
arrays, but this can be easily extended to cover that case.
```cpp
std::size_t M, N;

// 1D array:
std::array<int, 5> arr { 1, 4, 8, 3, 9 };
N = arr.size();

std::cout << "arr has " << N << " elements\n";

// 2D array:
std::array<std::array<int, 4>, 3> mat = {{
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
}};

M = mat.size();
N = mat[0].size();

std::cout << "mat has " << M << "x" << N << " elements\n";
```

The same exact function works for `std::vector`:
```cpp
std::vector<std::vector<int>> mat {{
    {1, 0, 4, 4, 5}, 
    {0, 1, 0, 7, 9}, 
    {0, 5, 1, 7, 3}
}};
const std::size_t M = mat.size(), 
                  N = mat[0].size();

std::cout << "mat has " << M << "x" << N << " elements\n";
```

> 📝 **Note**: Since C++17, there is a function named `std::size` ([see here](https://en.cppreference.com/w/cpp/iterator/size))
> which gets the size of an array (same restrictions apply to C-style arrays) _or_ a container. Specifically, if the object
> has a `.size()` method (as is the case with STL) then it calls it, otherwise if you have an array of the form `T arr[N]`
> where it returns $N$. There's also `std::ssize` **in C++20** in the same vein which returns a signed version of this. That is useful 
> in some circumstances where e.g. you have an `int` index type but `std::size` returns an unsigned integer, so the compiler will
> throw a warning reminding you that you have signed vs unsigned mismatch. I found a real use case for it here:
> ```cpp
> for (auto i = std::ssize(v) - 1; i >= 0; --i) {
>     std::cout << i << ": " << v[i] << "\n";
> }
> ```
> If you put `std::size(v)`, it will 1. fail if `v` has no elements and 2. it returns `std::size_t` which is unsigned,
> thus it can and _will_ underflow, so you'll never reach the condition. There is a dirty thing you can do:
> ```cpp
> for (auto i = std::size(v) - 1; i < std::size(v); --i)
> ```
> or
> ```cpp
> for (auto i = std::size(v) - 1; i-- > 0;)
> ```
> or, if you're willing to deal with warnings in your compiler, just put `i` as a large enough signed type. Perhaps do 
> `(int)(std::size(v) - 1)` or `static_cast<int>(std::size(v) - 1)` (the latter approach is more recommended in modern C++).
> I didn't think it's going to be this much of a mess, but I suppose the lesson is to use `std::ssize(v)` or take care
> when using `std::size(v)` (or `v.size()`).

Once we have the dimensions of the given array, let's see how to iterate. The classical way would be to use an index,
along with the size. This is useful if you actually need the index. I'll assume we have `M` and/or `N` using one of the
above methods. For illustration purposes, I'll showcase how to print arrays, which is a common operation:
```cpp
// 1D array:
for (std::size_t idx = 0; idx < N; ++idx) {
    std::cout << arr[idx] << " ";
}
std::cout << "\n";

// 2D array:
for (std::size_t row = 0; row < M; ++row) {
    for (std::size_t col = 0; col < N; ++col) {
        std::cout << mat[row][col] << " ";
    }
    std::cout << "\n"; 
    // ^ This is important, so we have a new 
    //   line after each row!
}
```

Oftentimes though, we don't care about the specific index, but the element, which is why we have the range-based for loop
starting from C++11, which works on any container and C-style arrays. If you've used a language with a for-each construct,
this is the C++ equivalent:
```cpp
for (const auto& elem : arr) {
    std::cout << elem << " ";
}

for (const auto& row : mat) {
    for (const auto& elem : row) {
        std::cout << elem << " ";
    }
    std::cout << "\n";
}
```
> 📝 **Note**: There are two things I've slipped in here: 
> 1. `auto` means that the compiler determines the type at compile time, which is useful for us because it means we don't
> have to deal with the type (which in some specific cases can be _really_ long). It also makes my example type-agnostic,
> so it works on anything from `int`s all the way to `std::array` or a complex class or whatever;
> 2. Usually we just want to use the element, not modify it, so we want to make it `const` whenever possible (`const T&` 
> should be your default, unless you have a good reason to modify the element). Also, if you omit the `&`, it copies it 
> by value, which is good for primitive types such as `int`, but not for everything else, since it's expensive to copy it.
> If you do want to modify the object, omit the `const`:
>   ```cpp
>   for (auto& elem : arr) {
>       elem *= 2;
>   }
>   ```
>   This opens up a way of reading an array or vector using this syntax:
>   ```cpp
>   for (auto& elem : arr) {
>       std::cin >> elem;
>   }
>   
>   for (auto& row : mat) {
>       for (auto& elem : row) {
>           std::cin >> elem;
>       }
>   }
>   ```

We can't talk about _adding_ or _removing_ elements from a static array, since its size is fixed. But for `std::vector`,
we have the `push_back()` and `pop_back()` methods:
```cpp
std::vector<int> v;
v.push_back(10);
v.push_back(20);
v.push_back(30);

std::cout << "[ ";
for (const auto& elem : v) {
    std::cout << elem << " ";
}
std::cout << "]\n";
// [ 10 20 30 ]

v.pop_back();
std::cout << "[ ";
for (const auto& elem : v) {
    std::cout << elem << " ";
}
std::cout << "]\n";
// [ 10 20 ]

// In order to store the element we're popping, we have to
// use back() (we also have the analogous front() for the first 
// element):
auto x = v.back();
v.pop_back();
std::cout << "[ ";
for (const auto& elem : v) {
    std::cout << elem << " ";
}
std::cout << "] " << x << "\n" ;
// [ 10 ] 20
```

We can "emulate" inserting an element in a C-style array by shifting the elements around (assuming we have enough elements):
```cpp
int A[5] = {1, 2, 3};
int N = sizeof(A) / sizeof(*A);

// Assuming you have something that delimits your current
// array. For the above case, that element's 0.
while (A[N - 1] == 0) {
    N--;
}
std::cout << "[ ";
for (size_t i = 0; i < N; ++i) {
    std::cout << A[i] << " ";
}
std::cout << "]\n";

// Now we have the actual number of elements currently present.
std::size_t idx;
do {
    std::cout << "Where do you want to insert the element?\n"
              << "(between 0 and " << N-1 << ")\n";

    std::cin >> idx;
    // std::size_t is unsigned, so it doesn't make sense to check
    // if idx < 0! You do need to do that check if idx's type is int.
    if (idx >= N) {
        std::cout << "Invalid index.\n";
        continue;
    }
} while (idx >= N);

int element;
std::cout << "What element do you want to insert?\n";
std::cin >> element;

// Here's the main algorithm:
if (idx == N-1) {
    // If we're at the end of the array, just add at the end
    // and increase the size;
    A[N++] = element; 
} else {
    // Else shift all elements from idx to the right and make room
    // for the new element.
    for (auto i = N; i > idx; --i) {
        A[i] = A[i - 1];
    }
    A[idx] = element;
    N++;
}

std::cout << "[ ";
for (size_t i = 0; i < N; ++i) {
    std::cout << A[i] << " ";
}
std::cout << "]\n";
```

This obviously works for `std::array` too. We can emulate deleting an element too:
```cpp
std::array<int, 10> A = {1, 65, 3, 99, 1, 65, 2, 98};
std::size_t N = A.size();

// [...]

if (idx == N-1) {
    // You can also just decrement N, but this makes it more
    // consistent with the rest.
    A[N--] = 0;  
} else {
    // Else shift all elements to the left
    for (std::size_t i = idx; i < N - 1; ++i) {
        A[i] = A[i + 1];
    }
    A[N--] = 0;
}

// [...]
```
We aren't really "deleting" the element, we're just pretending it doesn't exist. 

We can fully use the C++ STL to simplify part of this logic (you need `<algorithm>` for these):
```cpp
// Deleting
if (idx < N) {
    // Copy everything from the index...
    //      to the end of the array...
    //      at the index
    std::copy(std::begin(arr) + idx + 1, 
              std::end(arr), 
              std::begin(arr) + idx);
    
    // While overkill for a single element, it's useful
    // If you have several elements you want to remove.
    std::fill(std::end(arr) - 1, std::end(arr), 0);
    N--;
}

// Inserting
if (idx < N) {
    std::copy_backward(std::begin(arr) + idx,
                       std::end(arr) - 1,
                       std::end(arr));
    arr[idx] = value;
    N++;
}
```

On the other hand, if you have a `std::vector`, everything is, as is the theme for this entire article thus far, much
simpler (you also need `<algorithm>`):
```cpp
std::vector<int> v {1, 2, 3, 4, 5};

auto it = v.insert(std::begin(v), 200);
std::cout << *it << std::endl; // 200
// 200 1 2 3 4 5

v.insert(std::begin(v) + 2, 10);
// 200 1 10 2 3 4 5 

v.insert(std::end(v) - 1, 50);
// 200 1 10 2 3 4 50 5 

// std::next(it_begin, 3) == it_begin + 3
auto it_begin = std::begin(v);
v.insert(std::next(it_begin, 3), -10);
// 200 1 10 -10 2 3 4 50 5 

// std::prev(it_end, 2) == it_end - 2
auto it_end = std::end(v);
v.insert(std::prev(it_end, 2), 8);
// 200 1 10 -10 2 3 4 8 50 5

std::size_t idx = 4;
v.insert(v.begin() + idx, -100);
```
And for inserting multiple elements at once:
```cpp
std::vector<int> v {1, 2, 3, 4, 5};

// If you have them stored in a C-style array:
int A[] = {-5, -4, -3, -2, -1};
auto N = std::size(arr);
v.insert(std::begin(v) + 2, A, A + N);

for (const auto& elem : vec) {
    // 1 2 -5 -4 -3 -2 -1 3 4 5
    std::cout << elem << " ";
}
std::cout << std::endl;

// If you have them stored in a std::array or std::vector:
std::array<int, 10> B {10, 9, 8, 7, 6, 20, 18, 16, 14, 12};
v.insert(std::begin(v) + 1, std::begin(B), std::end(B));

for (const auto& elem : vec) {
    // 1 10 9 8 7 6 20 18 16 14 12 2 -5 -4 -3 -2 -1 3 4 5 
    std::cout << elem << " ";
}
std::cout << std::endl;

```

And now removing elements. C++ has an idiom called the erase-remove idiom (which does _somewhat_ work on static arrays...
with some caveats).
```cpp
std::vector<int> v {1, 2, 3, 4, 5, 50, 1, 1, 100, 7, 60, 8, 9, 1};

// Remove a single value
v.erase(std::remove(std::begin(v), std::end(v), 1),
        std::end(v)); // < Do **NOT** forget this!

for (const auto& elem : v) {
    // 2 3 4 5 50 100 7 60 8 9
    std::cout << elem << " "; 
}
std::cout << std::endl;

// Remove based on a predicate
v.erase(std::remove_if(std::begin(v), std::end(v),
                       [](const auto& x) { return x % 2 == 0; }),
        std::end(v));

// Alternatively, if you don't feel comfortable with lambdas, you
// can make a function like:
// bool isEven(const int x) { return x % 2 == 0; }
// and:
// v.erase(std::remove_if(std::begin(v), std::end(v), isEven), 
//         std::end(v));

for (const auto& elem : v) {
    // 3 5 7 9
    std::cout << elem << " "; 
}
std::cout << std::endl;
```

This works because `std::remove` doesn't actually _remove_ the items, but it moves the ones that should _not_ be deleted
to the front. This, in turn, means that it returns an iterator to the end of that range, and then `std::erase` can delete
everything from that position to the end (that's why that `std::end(v)` is necessary!) This also means that you can
make it work on a `std::array` or a C-style array:
```cpp
int a[] {0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377};

auto new_end = std::remove_if(std::begin(a), std::end(a), isOdd);
auto size = std::distance(std::begin(a), new_end);

for (size_t i = 0; i < N; ++i) {
    // 0 2 8 34 144
    std::cout << a[i] << " ";
}
std::cout << std::endl;

std::fill(new_end, std::end(a), 0);

for (const auto& e: a) {
    // 0 2 8 34 144 0 0 0 0 0 0 0 0 0 0
    std::cout << e << " ";
}
```

If you're working with `std::vector` specifically (which should be your go-to container anyway), in C++20 the wonderful 
overlords gave us `std::erase` and `std::erase_if` defined in `<vector>` which lets us do this:

```cpp
std::vector<int> nums {17, 20, 4, 6, 7, 19, 19, 13, 5};
std::erase(nums, 19);
auto erased = std::erase_if(nums, [](auto x) { return x & 1; });
```
> 📝 **Note**: Both `std::erase` and `std::erase_if` return the number of elements erased.
## Some basic algorithms
### Minimum and maximum element
Without `<algorithm>`:
```cpp
std::vector<int> values {6, 2, 1, 7, 12, 5};
int min = values[0], max = values[0];

for (const auto x : values) {
    if (x < min) {
        min = x;
    }
    // min = std::min(x, min);
    
    if (x > max) {
        max = x;
    }
    // max = std::max(x, max);
}

std::cout << "Min: " << min << ", max: " << max << "\n";
```
With `<algorithm>`, everything is nicer:
```cpp
std::vector<int> v {6, 2, 1, 7, 12, 5};
const auto minmax = std::minmax_element(std::begin(v), std::end(v));

std::cout << "Min: " << minmax.first << ","
          << "max: " << minmax.second << "\n";

// Or, with C++17:
const auto [min, max] = std::minmax_element(begin(v), end(v));
std::cout << *min << " " << *max << "\n";
```
You can also get just the minimum and maximum element:
```cpp
std::vector<int> v {6, 2, 1, 7, 12, 5};
const auto& min = std::min_element(std::begin(v), std::end(v));
const auto& max = std::max_element(std::begin(v), std::end(v));

std::cout << *min << " " << *max << "\n";
```
and their respective indices:
```cpp
std::vector<int> v {6, 2, 1, 7, 12, 5};
const auto [min, max] = std::minmax_element(begin(v), end(v));
std::cout << "Min is at "
          << "v[" << std::distance(std::begin(v), min) << "] "
          << "and max is at "
          << "v[" << std::distance(std::begin(v), max) << "]\n";
```
> 📝 **Note**: You can pass a comparison function to all the aforementioned functions, so you can compare by a specific 
> criterion. This can be useful when you have a struct that can't be easily compared otherwise or have specific
> requirements.
> The function (or lambda) needs to be of type:
> `bool cmp(const T& a, const U& b);`. You'll usually have `T == U` (so the types will be the same). `T` stands for 
> the type you're comparing.
> 
> Here's an example. Let's say you want to find the youngest and oldest person:
> ```cpp
> struct Person {
>    std::string name;
>    int age;
>
>    Person(std::string  n, int a) 
>       : name(std::move(n)), age(a) {}
> };
> 
> bool compareAge(const Person& p1, const Person& p2) {
>     return p1.age < p2.age;
> }
> 
> int main() {
>   std::vector<Person> people = {
>        {"Alice", 25},
>        {"Bob", 30},
>        {"Charlie", 22},
>        {"David", 35},
>        {"Eva", 28}
>    };
>
>    const auto [youngest, oldest] 
>       = std::minmax_element(std::begin(people), 
>                             std::end(people),
>                             compareAge);
>
>    std::cout 
>          << "Youngest: " 
>              << youngest->name
>              << " (" << youngest->age << ")\n"
>          << "Oldest: " 
>              << oldest->name
>              << " (" << oldest->age << ")\n";
> }
> ```

### Cyclic (or “circular”) permutations
We can also “rotate” an array (such a rotation is called a cyclic permutation) either to the left or to the right.

For instance, if we have:
```cpp
std::vector<int> nums{5, 16, 39, 19, 35, 1, 4, 1, 49};
```
then all the cyclic permutations to the left would be:
```
16 39 19 35 1 4 1 49 5 
39 19 35 1 4 1 49 5 16 
19 35 1 4 1 49 5 16 39 
35 1 4 1 49 5 16 39 19 
1 4 1 49 5 16 39 19 35 
4 1 49 5 16 39 19 35 1 
1 49 5 16 39 19 35 1 4 
49 5 16 39 19 35 1 4 1 
5 16 39 19 35 1 4 1 49
```
and to the right:
```
49 5 16 39 19 35 1 4 1 
1 49 5 16 39 19 35 1 4 
4 1 49 5 16 39 19 35 1 
1 4 1 49 5 16 39 19 35 
35 1 4 1 49 5 16 39 19 
19 35 1 4 1 49 5 16 39 
39 19 35 1 4 1 49 5 16 
16 39 19 35 1 4 1 49 5 
5 16 39 19 35 1 4 1 49 
```

This is how we would do it without `<algorithm>`:
```cpp
std::vector<int> nums{5, 16, 39, 19, 35, 1, 4, 1, 49};

bool rotate_left = true;

const auto N = std::ssize(nums);

for (std::size_t i = 0; i < N; ++i) {
    if (rotate_left) {
        const auto temp = nums.front();
        for (std::size_t j = 0; j < N - 1; ++j) {
            nums[j] = nums[j + 1];
        }
        nums.back() = temp;
    } else {
        const auto temp = nums.back();
        for (auto j = N - 1; j > 0; --j) {
            nums[j] = nums[j - 1];
        }
        nums.front() = temp;
    }

    for (const auto& e : nums) {
        std::cout << e << " ";
    }
    std::cout << "\n";
}
```
and with `<algorithm>` and `std::rotate` (I'll only modify the `if`):
```cpp
if (rotate_left) {
    std::rotate(std::begin(nums), 
                std::begin(nums) + 1, 
                std::end(nums));
} else {
    // begin -> rbegin, end -> rend
    // It is literally the rotate left algorithm
    // but in reverse.
    std::rotate(std::rbegin(nums), 
                std::rbegin(nums) + 1, 
                std::rend(nums));
}
```

This approach also generalizes to any $k < N$:
```cpp
std::rotate(std::begin(nums), 
            std::begin(nums) + k, 
            std::end(nums));
```
`std::rotate` has three arguments: the beginning of the original range, the element that should appear at the beginning
of the rotated range (if you're shifting by $k$, that should be `nums[k]` a.k.a. `std::begin(nums) + k`) and the end of 
the original range.

> ⚠️ **Warning**: C++20 has two seemingly useful algorithms for shifting elements: `std::shift_left` and `std::shift_right`.
> While those _do_ shift elements, and you can give a $k$ to indicate how many positions to shift, it doesn't have the same
> effect as `std::rotate`. It's almost like a move, not like a `std::rotate`:
> ```cpp
> std::vector<int> data{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
> std::shift_left(std::begin(data), std::end(data), 3);
> // 4 5 6 7 8 9 10 8 9 10 
> 
> data = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
> std::shift_right(std::begin(data), std::end(data), 3);
> // 1 2 3 1 2 3 4 5 6 7
> ```
> I have to mention that if $k \leq 0$ or $k \geq N$, then it doesn't have any effect. Also, the standard doesn't specify
> the state of the shifted values. `std::rotate` is almost like storing the first/last $N - k$ elements, shifting the 
> elements and then copying the old range back into the array, but it's more pain that it should be. Just letting you know
> that `std::shift_left` or `std::shift_right` might _not_ be what you need.

### Reversing an array
That is simple to do, so I'll show both the non-STL and the STL approach:
```cpp
std::vector<int> nums{20, 9, 42, 43, 48, 37, 49, 22, 15};

// Without STL:
const auto N = std::ssize(nums);
for (int i = 0; i < N/2; ++i) {
    const auto temp = nums[i];
    nums[i] = nums[N - i + 1];
    nums[N - i + 1] = temp;
}

for (const auto& e : nums) {
    std::cout << e << " ";
}
std::cout << "\n";

// With STL:
std::reverse(std::begin(nums), std::end(nums));
for (const auto& e : nums) {
    std::cout << e << " ";
}
std::cout << "\n";
```
> 📝 **Note**: Instead of using a temporary variable, you can use `std::swap(nums[i], nums[N-i+1]);`.

### Merging two sorted arrays
There are situations where you might want to merge two arrays (there's even a famous sorting algorithm using this exact
technique). It's important that these arrays are **sorted**, otherwise this wouldn't work. I think it's obvious that they
should be sorted in the same order too.

Without the STL:
```cpp
std::vector<int> A { 3, 7, 10, 11, 16, 22, 32, 33, 38 };
std::vector<int> B { 3, 3, 12, 16, 22, 39, 40, 44, 50 };

// The resulting vector has to fit both A and B, so
// its size is the sum of the sizes of A and B.
const std::size_t M = std::size(A), 
                  N = std::size(B);
std::vector<int> result(M + N);

std::size_t i = 0, j = 0, k = 0;

while (i < M && j < N) {
    if (A[i] < B[j]) {
        result[k++] = A[i++];
    } else {
        result[k++] = B[j++];
    }
}
while (i < M) {
    result[k++] = A[i++];
}

while (j < N) {
    result[k++] = B[j++];
}

// result is:
// 3 3 3 7 10 11 12 16 16 22 22 32 33 38 39 40 44 50
```

The main idea (and how I like to remember it) is like this:
1. We do a first pass, where we go through both arrays simultaneously, and at each step the while loop chooses the
   smaller element between $A_i$ and $B_j$. If $A_i$ is smaller, this means that it should be the next in the result
   array, since we're building the result in order, otherwise we're adding $B_j$.
2. There's a possibility we might still have elements that we didn't add, either because $i$ reached the end or $j$ did.
   In that case, just add the remaining elements from $A$ if that's the case, then the $B$ elements (since we know that
   the elements left have to be in increasing order _and_ have to follow each other).

> 📝 **Note**: In the case that the `result[k++] = A[i++]` syntax seems strange, it does this:
> ```cpp
> k++;
> result[k] = A[i];
> i++;
> ```
> so we're first moving the next position, then assigning it to the array element in either $A$ or $B$, then moving that
> array's index.

With STL, we have `std::merge`:
```cpp
std::vector<int> A { 3, 7, 10, 11, 16, 22, 32, 33, 38 };
std::vector<int> B { 3, 3, 12, 16, 22, 39, 40, 44, 50 };

std::vector<int> result;

std::merge(std::begin(A), std::end(A),
           std::begin(B), std::end(B),
           std::back_inserter(result));
```

> 📝 **Note**: `std::back_inserter` is an output iterator for inserting at the end of a container (`std::vector` in this
> case). There are multiple such output iterators. A fun one in `<iterator>` is `std::ostream_iterator` that can let you
> print the array without storing it:
> ```cpp
> std::merge(std::begin(A), std::end(A),
>            std::begin(B), std::end(B),
>            std::ostream_iterator<int>(std::cout, " "));
> ```

> 📝 **Note**: As you may have seen from the output of the merge algorithm, it keeps duplicated elements, which is why
> you need exactly $M + N$ elements. Thus, it isn't strictly speaking the same as the union of $A$ and $B$. For a true
> set union, you have `std::set_union`:
> ```cpp
> std::vector<int> A { 3, 7, 10, 11, 16, 22, 32, 33, 38 };
> std::vector<int> B { 3, 3, 12, 16, 22, 39, 40, 44, 50 };
> 
> std::vector<int> result;
> 
> std::set_union(std::begin(A), std::end(A),
>                std::begin(B), std::end(B),
>                std::back_inserter(result));
> // 3 3 7 10 11 12 16 22 32 33 38 39 40 44 50
> ```
> The difference is in how they handle values from both input ranges which compare equivalent. If you have a value that
> repeats $m$ times in $A$ and $n$ times in $B$, you would see it $m + n$ times with `std::merge` and $\max (m, n)$ times
> with `std::set_union`. I am not quite sure what's the reasoning, maybe it is to keep $A \cup B = (A \setminus B) \cup (B \setminus A) \cup (A \cap B)$,
> I am not sure. If you really need the elements to be unique, then you can use our dear friend `std::erase`:
> ```cpp
> result.erase(std::unique(std::begin(result), std::end(result)),
>              std::end(result));         
> ```
> While you're here, check `std::set_intersection`, `std::set_difference`, `std::set_symmetric_difference` and 
> `std::includes` for more set-related things, as well as `std::set` and `std::unordered_set` as their own containers.

### Miscellaneous operations
This will be just a cursory glance, since it's not part of the main article. Unless I mention otherwise, all examples 
require `<algorithm>`:
#### Modifying an array
```cpp
std::vector<int> A { 3, 7, 10, 11, 16, 22, 32, 33, 38 };
std::vector<int> B { 3, 3, 12, 16, 22, 39, 40, 44, 50 };

std::for_each(std::begin(A), std::end(A),
              [](auto& x) { x %= 10; });

std::for_each(std::begin(A), std::end(A),
              [](const auto& x) { std::cout << x << " "; });
std::cout << "\n";
// 3 7 0 1 6 2 2 3 8

// For simply transforming an array, such as in the first
// for_each, you have std::transform:
std::vector<int> res;
std::transform(std::begin(B), std::end(B),
               std::back_inserter(res),
               [](const auto& x) { return x * 3; });

for (const auto& e : res) {
    std::cout << e << " ";
}
std::cout << "\n";
// 9 9 36 48 66 117 120 132 150
```
#### Reducing an array
This requires `<numeric>` (and `<string>` for the last examples):
```cpp
std::vector<int> A { 3, 18, 24, 17, 6, 40, 5, 30, 16 };
std::vector<int> B { 5, 23, 2, 17, 7, 35, 40, 20, 12 };

// std::accumulate and std::reduce are your
// best friends in this case!

auto sum = std::accumulate(std::begin(A), std::end(A), 
                           0UL,
                           std::plus<>{});
std::cout << "Sum of A: " << sum << "\n";

auto product = std::accumulate(std::begin(A), std::end(A), 
                               1UL,
                               std::multiplies<>{});
std::cout << "Product of A: " << product << "\n";

auto diff = std::accumulate(std::begin(B), std::end(B), 
                            0,
                            std::minus<>{});
std::cout << "Difference of B: " << diff << "\n";

auto concatenated
    = std::accumulate(std::begin(B), std::end(B),
                      std::string{},
                      [](const auto& x, const auto& y) {
                          auto z = std::to_string(y);  
                          return "(" + x + " " + z + ")";
                      }); 
std::cout << "B concatenated: " << concatenated << "\n";

// The sum can be achieved by std::reduce as well:
sum = std::reduce(std::begin(A), std::end(A), 
                  0UL, std::plus<>{});
std::cout << "Sum of A: " << sum << "\n";

// and the product too:
product = std::reduce(std::begin(A), std::end(A), 
                      1UL,
                      std::multiplies<>{});
std::cout << "Product of A: " << product << "\n";

// But the difference doesn't give the same result!
diff = std::reduce(std::begin(B), std::end(B), 
                   0,
                   std::minus<>{});
std::cout << "Difference of B: " << diff << "\n";

// And std::reduce expects the same types on the arguments,
// so I'll transform the numbers as strings before proceeding:
std::vector<std::string> strs;
std::transform(std::begin(B), std::end(B),
               std::back_inserter(strs),
               [](const auto& x) { return std::to_string(x); });

concatenated
    = std::reduce(std::begin(strs), std::end(strs),
                  std::string{},
                  [](const auto& x, const auto& y) {
                      return "(" + x + " " + y + ")";
                  }); 
std::cout << "B concatenated: " << concatenated << "\n";
```
The output is:
```
Sum of A: 159
Product of A: 12690432000
Difference of B: -161
B concatenated: ((((((((( 5) 23) 2) 17) 7) 35) 40) 20) 12)
Sum of A: 159
Product of A: 12690432000
Difference of B: 39
B concatenated: ((( ((5 23) (2 17))) ((7 35) (40 20))) 12)
```

Why don't we get the same results across the board? The string examples should give you a clue. Specifically, look at how
the parentheses are put. The order of execution is different. With `std::accumulate`, it's run serially, so it is essentially
like a for loop, while `std::reduce` (which came in C++17) is run in parallel (which is why it exists, it can also take another argument that
I'll talk about after this). `std::reduce` requires the operation to both be associative _and commutative_ (if you have
$f$, then $f(a, b)$ = $f(b, a)$). Commutativity is important because it allows the compiler to do divide and conquer
and execute the operations in whatever order it thinks is the best. Meanwhile, `std::accumulate` runs from left to right.
Even if the given operation (which is by default `std::plus<>{}` in both cases) is associative and commutative, 
`std::reduce` will be faster because of the aforementioned parallelism. This is how `std::accumulate` works (taking `-` 
as an example):
```
  ((((((((0 - 5) - 23) - 2) - 17)  - 7) - 35) - 40) - 20) - 12
= (((((((-5 - 23) - 2) - 17)  - 7) - 35) - 40) - 20) - 12
= ((((((-28 - 2) - 17)  - 7) - 35) - 40) - 20) - 12
= (((((-30 - 17)  - 7) - 35) - 40) - 20) - 12
= ((((-47 - 7) - 35) - 40) - 20) - 12
= (((-54 - 35) - 40) - 20) - 12
= ((-89 - 40) - 20) - 12
= (-129 - 20) - 12
= -149 - 12
= -161
```
while this is how `std::reduce` works:
```
  ((0 - ((5 - 23) - (2 - 17))) - ((7 - 35) - (40 - 20))) - 12
= ((0 - ((-18) - (-15))) - ((-28) - (20))) - 12
= ((0 - (-3)) - (-48)) - 12
= (-3 - (-48)) - 12
= 45 - 12
= 39
```

Once $N$ is large enough, this makes a huge difference in performance. Use `std::accumulate` _only_ if your operation
isn't commutative.
> 📝 **Note**: `std::reduce` came in C++17, and with that version we also have execution policies (found in `<execution>`).
> They specify _how_ an algorithm is being executed. In order, we have:
> - `std::execution::seq` which specifies that the algorithms should be executed sequentially. This is the default.
> - `std::execution::par` specifies that the algorithm should run in parallel, i.e. in multiple threads. The standard
>   doesn't specify how many threads, but it has to be more than one. This _can_ introduce overhead (so you shouldn't prefer
>   it for small data as it can be slower than its sequential counterpart), and can introduce race conditions.
> - `std::execution::par_unseq`: same as above, but it also can produce non-deterministic results. The order in which the
>   elements are processed is not guaranteed. On the other hand, this also introduces vectorization and can take advantage
>   of SIMD and other hardware and software features. It's not suitable for all tasks and may not be supported on all
>   hardware, but it shouldn't be that big of a deal on your computer. 
> - `std::execution::unseq` (C++20): same as `par_unseq` but without parallelism. This means that the algorithm may be executed
>   on a single thread using instructions that operate on multiple data items (SIMD). 
> 
> A lot of algorithms in the STL now take execution policies as their first arguments, including all the ones we've 
> seen during this article, so I invite you to read up for yourself. :)

There are some algorithms I haven't mentioned, such as `std::transform_reduce`, `std::inner_product`, `std::iota`, 
`std::adjacent_difference` etc., but you can look up what's in `<numeric>` (and `<algorithm>`, you'll find other functions
you can use to simplify common tasks).