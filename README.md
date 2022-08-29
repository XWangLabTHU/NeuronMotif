
# NeuronMotif

This repository implements the NeuronMotif algorithm in ["NeuronMotif: Deciphering cis-regulatory codes by layerwise de-mixing of deep neural networks"](https://www.biorxiv.org/content/10.1101/2021.02.10.430606v1) by Zheng Wei et al.

This repository includes the code for generating the result in the paper. We also provide the instructions for users to apply NeuronMotif to their own models. 

Feel free to contact Zheng Wei for any issues or difficulties:
+ Email: weiz(at)tsinghua.edu.cn
+ GitHub: https://github.com/wzthu/NeuronMotif/issues

The code for training the deep convolutional neural network (DCNN) models that are used in this work are stored in [dcnn](https://github.com/wzthu/NeuronMotif/tree/master/dcnn). If you do not want to train DCNN models, you can ignore this folder.

The code implements the NeuronMotif algorithm for decoupling the mentioned DCNN **once** are stored in [nm](https://github.com/wzthu/NeuronMotif/tree/master/nm). It also includes interpreting and visualizing codes. NeuronMotif only needs a weight file of the DCNN. We provide the links to download the weight file of the DCNN models used in this paper. Users can feed their own DCNN models to NeuronMotif after they make some changes to the folder [code](https://github.com/wzthu/NeuronMotif/tree/master/nm/code) following the instructions in [nm](https://github.com/wzthu/NeuronMotif/tree/master/nm). The existing DCNN models in the paper are also examples to used NeuronMotif.


In brief, there are two steps for a DCNN model. Take demo2 as an example.

1. Training model:[dcnn/demo/demo2](https://github.com/wzthu/NeuronMotif/tree/master/dcnn/demo/demo2)(optional if model is trained).
2. Run NeuronMotif algorithm: [nm/demo/demo2](https://github.com/wzthu/NeuronMotif/tree/master/nm/demo2)



The code of NeuronMotif does not depend on GPU. We have parallelized the code so that it can make full use of the computing resources in a computer cluster. Some scripts can be submitted to different nodes in a computer cluster at the same time. See the instructions in code folders. 

If you are interested in a part of the work, you can read README file in the corresponding folder for the instruction of downloading the data and running the code.

Before using this repository, users should install the dependent software following the instruction at the end of this file.

# Introduction of NeuronMotif

NeuronMotif is an algorithm for interpreting the patterns learned by deep convolutional neurons (DCN) in DCNN. For a DCNN based on DNA sequences, it can convert the substructure weight of a DCN into DNA sequence motifs. DNA can be considered a new language so the task of NeuronMotif is to uncover the motif and motif grammar embedded in DCNs.

![](https://github.com/wzthu/NeuronMotif/blob/master/Goal.jpg)

# Results of NeuronMotif

Result is available at [NeuronMotif website](https://wzthu.github.io/NeuronMotif/).


# Installation

We test this repository in a CentOS 7 computer cluster with 4 nodes, each of which contains 28 cores and 128 GB memory. About 10 TB is consumed for obtaining the result of all examples in the manuscripts. The installation lasts for ~10 min if there are no more dependent packages.

## Install anaconda

Download and install (anaconda)[https://www.anaconda.com/products/individual].

## Create the  NeuronMotif environment

NeuronMotif is implemented and tested in python 3.6.

```
conda create -n NeuronMotif python=3.6
```

## Install dependent packages

```
conda activate NeuronMotif
pip install h5py==2.10.0
pip install matplotlib
pip install pandas
pip install numpy
pip install sklearn
pip install tensorflow==1.15.0
pip install keras==2.3.1

```


## Install visualization dependences

Download and install meme-suit to get tomtom first:

version: 5.1.0, later version does not support >100 bp receptive field.

Download:

```
wget https://meme-suite.org/meme/meme-software/5.1.0/meme-5.1.0.tar.gz

```

Install:


```
tar zxf meme-5.1.0.tar.gz
cd meme-5.1.0
./configure --prefix=$HOME/meme --enable-build-libxml2 --enable-build-libxslt
```

***Note: if there are some warnings in the configuring, HTML related perl dependent should be solved:***

File::Which missing.

HTML::Template missing.

HTML::TreeBuilder missing.

JSON missing.

These warnings can be solved by:
```
export PERL_MM_USE_DEFAULT=1
perl -MCPAN -e 'install "File::Which"'
perl -MCPAN -e 'install "HTML::Template"'
perl -MCPAN -e 'install "HTML::TreeBuilder"'
perl -MCPAN -e 'install "JSON"'
perl -MCPAN -e 'install "XML::Simple"'
perl -MCPAN -e 'install "XML::Parser::Expat"'
```

Compile the code:

```
make
make test
make install
```
***Note: make sure tomtom in the meme suit can work in the make test.***

The erros of other tools can be ignored.

Add it to PATH environment variable by appending following command line to  ~/.bashrc:

```
export PATH=$HOME/meme/bin:$HOME/meme/libexec/meme-5.1.0:$PATH
```

and execute:

```
source  ~/.bashrc
```

Test following commands:

```
tomtom
```
and

```
chen2meme  -h
```

## Clone this repository:

```
git clone https://github.com/wzthu/NeuronMotif
```


## Ready to use

This command line should be executed every time you enter the terminal before using NeuronMotif

```
conda activate NeuronMotif
```
