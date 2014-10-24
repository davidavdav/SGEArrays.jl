SGEArrays.jl
===========
[![Build Status](https://travis-ci.org/davidavdav/SGEArrays.jl.svg)](https://travis-ci.org/davidavdav/SGEArrays.jl)

SGEArray implements a simple iterator in Julia to efficiently handle Sun Grid Engine task arrays

Synopsis
--------

Julia main:

```julia
using SGEArrays

listfile = ARGS[1]
files = readdlm(listfile)

for file in SGEArray(files)
  ## process file $file 
end
```

bash call, submit an SGE array job as an array of size 80

```bash
find data/input/ -type f > filelist
qsub -t1:80 -b y -cwd bin/julia-script filelist
```

The first job in the array processes files[1], files[81], etc, the second job processes files[2], files[82], etc.  

If the julia script is called outside the context of an SGE array, the iterator simply iterates over all elements. 


