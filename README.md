# Implicit Skinning
This is my Advanced Graphics Software Development Techniques assignment for Bournemouth University.
This project is my implementation of implicit skinning based on ["Implicit Skinning: Real-Time Skin Deformation with Contact Modeling"](http://rodolphe-vaillant.fr/pivotx/templates/projects/implicit_skinning/implicit_skinning.pdf). 
The project is written in C++ and uses CUDA to speed up evaluation of field functions as well as perform skinning computations
## How it Works
A model is segmented into mesh parts, each mesh part is determined by the underlying bone structure and the bone weights for each vertex. 
Then sample points on the surface of each mesh part is generated. 
From these sample points a compactly supported [0-1] field function is generated, the 0.5 iso-surface of this field function closely approximates the original mesh part.
Durinig animation each mesh part is rigidly transformed by the corresponding bone. The field function is also transformed.
The transformed field functions are combined using composition operators that combines two field functions into one.
Once all the fields are composed together we are left with the global field, whose 0.5 iso-surface approximates the whole mesh.
During the skinining process we initially apply LBW skinning, then we march the deformed vertices along the gradient of the global field.
We apply some smoothing and eventually are left with  


## Docs
To build the documentation using Doxygen, run:
```bash
doxygen Doxyfile
```

## Supported Platforms
This project has only been tested on Linux, Ubuntu 16.04 and CentOS.

Requires an NVIDIA CUDA enabled GPU to utilize parallel optimizations.


## Dependencies
| **Name** | **Version** |
| ---- | ------- |
| [CUDA](https://developer.nvidia.com/cuda-downloads) | >= 7 |
| [GLM](http://glm.g-truc.net/0.9.8/index.html)| >= 0.9.2 (tested 0.9.8) |
| [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page)| >= 3.2.9 |
| [ASSIMP](http://www.assimp.org/) | >= 3.3.1 |


## Install and Build
```bash
git clone https://github.com/IdrisMiles/ImplicitSkinning.git
cd ImplicitSkinning
qmake
make clean
make
```

## Run
```bash
cd ImplicitSkinning/bin
./app
```

## Usage
Load in an aniimatio file.
### Accepted Animation Files Format
* .dae (COLLADA) - tested
### Key Operations
* **W** - Toggle skinned mesh wireframe
* **E** - Toggle rendering skinned mesh
* **R** - Toggle rendering Iso-Surface of global field
* **T** - Toggle between Implicit Skinning and Linear Blend Weight Skinning

## Version
This is version 0.1.0

## Author

## License
