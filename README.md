## arrfunc

This package provides a class ArrayFunc representing vector-valued functions of vector-valued inputs which may be treated
as NumPy arrays in many ways including
- Slicing
- Addition
- Multiplication
- Outer product
- Linear algebra operations such as determinant and inverse (if the shape is appropriate)

In particular, ArrayFunc objects may have arbitrary output shape, and their input shape must be of the form `(N, ...)`, where
`N` is the dimension of the input space. The function is assumed to vectorize over all additional indices provided in the
input.

## Examples

To construct an ArrayFunc, three inputs are needed:
- A function which vectorizes appropriately.
- The shape of the output of the function.
- The dimension `N` of the input.

So for example:
```
f = ArrayFunc(lambda x: x[0][np.newaxis], [1], 2)
```
Here `f` returns the first component of the two-dimensional input.

For a more sophisticated example:
```
f = ArrayFunc(lambda x: np.array([[x[0],x[1]],[x[0],x[1]]]), [2,2], 2)
```
Here `f` returns a (2,2) array formed of concatenating the two-dimensional input to itself.

In the following example, f and k are ArrayFuncs and g and h return the outer products of their output.
```
f = ArrayFunc(lambda x: x[0][np.newaxis], [1], 2)
k = ArrayFunc(lambda x: np.array([[x[0],x[1]],[x[0],x[1]]]), [2,2], 2)

g = k*f
h = f*k
```

In the following example, k is an ArrayFunc and q returns the result of slicing its output:
```
k = ArrayFunc(lambda x: np.array([[x[0],x[1]],[x[0],x[1]]]), [2,2], 2)
q = k[0:1]
```

## License

This package is available under an MIT license.
