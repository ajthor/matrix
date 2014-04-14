# Matrix.js

Matrix math utility for JavaScript.

Matrix.js is a custom library developed to address the need for 
certain matrix math functions in Javascript. This custom class 
implements several mathematical functions ranging from basic 
addition and subtraction to some more programmer-oriented 
functions such as the hadamard (element-wise) product.

## Installing Matrix.js

Install matrix.js via:

    npm install git://github.com/ajthor/matrix

Once matrix.js is imported into your project, you can use Matrix.js
by creating a new Matrix object (new keyword is optional).

    var Matrix = require("matrix");

    var M = new Matrix([3, 3]);

## Functions

Matrix.js implements several functions for manipulating matrices, 
including:

- Addition, subtraction, and multiplication by scalars and other matrices.
- Finding the transpose matrix.
- Dot product multiplication.
- Raising matrices to (positive) powers.

## Usage

All matrix objects are created using `Matrix(dimensions)`. 

    var M = Matrix([3,3]);
    
Similarly, you can pass a nested array containing values to 
the Matrix. All nested arrays should be the same size.

    var A = Matrix([ [ 1, 2 ],
                     [ 3, 4 ] ]);
                     
    var B = Matrix([ [ 5, 6 ],
                     [ 7, 8 ] ]);
                     
### Accessing items in the matrix

All matrix values are stored in the `Matrix.value` property of the matrix.
They can be accessed directly, by using the `Matrix.value[row][col]` syntax,
Or, they can be accessed using the `Matrix.get(row, col)` function.

Similarly, in order to set a value in a matrix, there is a `Matrix.set()` function.

    A.get(0, 0); // 1
    A.set(0, 0)(4); 
    
    /* Or, alternately */
    
    A.value[0][0]; // 4
    A.value[0][0] = 1;
    
### Matrix properties

Matrices have several properties which give the dimensions of the matrix,
such as `Matrix.rows`, `Matrix.cols`, and `Matrix.dimensions`.

Aside from this, it has an __identity__ property and a __transpose__ property.

    A.T; // Returns a new matrix object with transposed values of A.
    A.I; // Returns a new matrix object which is the identity matrix of A.
    
## Matrix Math Functions

Because JavaScript doesn't support operator overloading, there are a number
of matrix math functions available either from the Matrix super object itself,
or from a Matrix instance.

The main difference is that if you call the function from the super object, it
returns a new matrix. 

If you call it from the instance, it returns `this` to allow for chaining.

    var result = Matrix.add(A, B); // result.value is [[6, 8],[10, 12]], A and B unchanged.
    
    A.add(B); // A.value changes to [[6, 8],[10, 12]]
    
In this way, you can use all of the Matrix math functions:

- `add` - Can add scalars and matrices together.
- `sub` - Can subtract scalars and matrices from each other. *Be careful with the syntax here. `Matrix.sub(3, A, B)` equates to __3__ - __A__ - __B__.
- `dot` - Can compute the dot product of matrices. (Prototype function can only accept matrices of the same, square dimensions)
- `product` - Can multiply scalars and matrices together. (Default is dot product for matrix multiplication)
- `mult` - Can multiply matrices together using Hadamard (element-wise) multiplication. The element-wise product is a product which multiplies straight across. Element *ij* in matrix __A__ is multiplied by element *ij* in matrix __B__.
- `pow` - Can raise matrices to (positive) powers or 0. (Inverse multiplication is not yet supported)

### Example usage:

    A = Matrix([[1,2],[3,4]]);
    B = Matrix([[5,6],[7,8]]);
    
    A.product(3, B).add(4);
    
    B.get(1,0); // 7
    
    var result = Matrix.product(A.T, B);
    
    result = Matrix.product(A, A.I); // A
    
