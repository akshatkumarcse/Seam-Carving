# Implementation of Seam Carving Algorithm for Content-Aware Image Resizing

* Paper: [Seam carving for content-aware image resizing](https://dl.acm.org/doi/10.1145/1275808.1276390)

For more information on how the algorithm works, see my [blog post](https://akshatkumarcse.github.io/post/seam-carving-algorithm/).

## Requirements
* OpenCV
* scipy
* numba
* numpy


## Usage
```
python seam_carving.py (-resize | -remove) -im <IM_PATH> -out <OUTPUT_IM_NAME> 
                       [-mask <MASK_PATH>] [-rmask <REMOVAL_MASK_PATH>] [-dy <DY>] [-dx <DX>] 
                       [-vis] [-hremove] [-backward_energy]
```

There are two modes of operations: `resize` or `remove`. The former is for resizing an image vertically or horizontally and the latter is for removing an object as specified by a mask.

For both modes:
* `-im`: The path to the image to be processed.
* `-out`: The name for the output image.
* `-mask`: (Optional) The path to the protective mask. The mask should be binary and have the same size as the input image. White areas represent regions where no seams should be carved (e.g. faces).
* `-vis`: If present, display a window while the algorithm runs showing the seams as they are removed.
* `-backward_energy`: If present, use the backward energy function (i.e. gradient magnitude) instead of the forward energy function (default).

For resizing:
* `-dy`: Number of horizontal seams to add (if positive) or subtract (if negative). Default is 0.
* `-dx`: Number of vertical seams to add (if positive) or subtract (if negative). Default is 0.

For object removal:
* `-rmask`: The path to the removal mask. The mask should be binary and have the same size as the input image. White areas represent regions to be removed.
* `-hremove`: If present, perform seam removal horizontally rather than vertically. This will be more appropriate in certain contexts.


#### Additional Parameters
There are some additional constants defined at the top of the code `seam_carving.py` that may be modified.
* The code currently downsizes any images with width larger than 500 pixels to 500 pixels for super fast carving. To change this, change the value of `DOWNSIZE_WIDTH`, or set `SHOULD_DOWNSIZE` to `False` to disable downsizing completely.
* Seams are visualized as a bluish-white color; change the color by changing the `SEAM_COLOR` array (in BGR format).


## Acknowledgements
Many parts of the python code are adapted from other implementations:
* https://github.com/axu2/improved-seam-carving
* https://github.com/andrewdcampbell
* https://github.com/vivianhylee/seam-carving
* https://karthikkaranth.me/blog/implementing-seam-carving-with-python/
