The
[notMNIST dataset](http://yaroslavvb.blogspot.com/2011/09/notmnist-dataset.html)
is a image recognition dataset of font glypyhs for the letters A
through J useful with simple neural networks. It is quite similar to
the classic [MNIST dataset](http://yann.lecun.com/exdb/mnist/) of
handwritten digits 0 through 9.

Unfortunately, the notMNIST data is not provided in the same format as
the MNIST data, so you can't just swap in the notMNIST data files and
run your neural network on it unaltered. This python script fixes
that. It converts a sample of the notMNIST dataset into the same file
format used by the MNIST dataset and outputs files that you can drop
directly into your existing program so that you can test that program
with the more challenging notMNIST letter glpyhs.

Instructions:

1) if you already have a MNIST data/ directory, rename it and create a
new one with code like this:

```sh
mv data data.original_mnist
mkdir data
```

2) Download and unpack the notMNIST data. The files are not
particularly large, but unpacking them can take a long time
because there are well over 500,000 individual image files.

```sh
curl -o notMNIST_small.tar.gz http://yaroslavvb.com/upload/notMNIST/notMNIST_mall.tar.gz
curl -o notMNIST_large.tar.gz http://yaroslavvb.com/upload/notMNIST/notMNIST_arge.tar.gz
tar xzf notMNIST_small.tar.gz
tar xzf notMNIST_large.tar.gz
```

3) Finally, run this script to convert the data to MNIST files in your
data/ directory and compress them:

```sh
python convert_to_mnist_format.py notMNIST_small 1000 data/t10k-labels-idx1-uyte data/t10k-images-idx3-ubyte
python convert_to_mnist_format.py notMNIST_large 6000 data/train-labels-idx1-byte data/train-images-idx3-ubyte
gzip data/*ubyte
```

The first command line above says that the test files should include
1000 entries for each of the 10 letters, and that the training files
should include 6000 entries for each of the 10 letters. This matches
the size of the MNIST files.  notMNIST is significantly bigger than
MNIST, however, and you can probably use numbers as large as 1800 for
the test files and 50000 for the training files.

The script chooses a random sample of notMNIST glyphs, but sets the
random seed so that it produces the same sample on each run.  If you
remove the random.seed() call you can produce different
MNIST-compatible data sets on each run.
