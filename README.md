# Sophus - Lie Groups Library

A C++ implementation of Lie groups (SO2, SE2, SO3, SE3, Sim3, ScSO3) using Eigen.

## Prerequisites

### Install Eigen3

Sophus requires Eigen3 for linear algebra operations. Install it using apt:

```bash
sudo apt update
sudo apt install libeigen3-dev
```

This will install Eigen3 headers to `/usr/include/eigen3`.

## Build and Install

```bash
git clone https://github.com/fynngwu/sophus_a621ff.git Sophus
cd Sophus
mkdir build && cd build
cmake ..
make -j$(nproc)
sudo make install
```

This will install:
- Headers to `/usr/local/include/sophus/`
- Library to `/usr/local/lib/libSophus.so`
- CMake config to `/usr/local/share/Sophus/`

## Using Sophus in Your CMake Project

After installation, you can use Sophus in your CMake projects:

### CMakeLists.txt Example

```cmake
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
PROJECT(MyProject)

# Find Sophus package (automatically finds Eigen3 dependency)
FIND_PACKAGE(Sophus REQUIRED)

# Include Sophus headers (includes Eigen3 headers too)
INCLUDE_DIRECTORIES(${Sophus_INCLUDE_DIRS})

# Create your executable
ADD_EXECUTABLE(my_app main.cpp)

# Link against Sophus library
TARGET_LINK_LIBRARIES(my_app ${Sophus_LIBRARIES})
```

### C++ Code Example

```cpp
#include <iostream>
#include <sophus/so3.h>
#include <sophus/se3.h>

using namespace Sophus;

int main() {
    // Create a rotation (SO3)
    SO3 R = SO3::exp(Vector3d(0.2, 0.5, 0.1));
    std::cout << "Rotation matrix:\n" << R.matrix() << std::endl;
    
    // Create a transformation (SE3)
    Vector3d t(1, 0, 0);
    SE3 T(R, t);
    std::cout << "Transformation matrix:\n" << T.matrix() << std::endl;
    
    // Transform a point
    Vector3d p(1, 2, 3);
    Vector3d p_transformed = T * p;
    std::cout << "Transformed point: " << p_transformed.transpose() << std::endl;
    
    return 0;
}
```

### Build Your Project

```bash
mkdir build && cd build
cmake ..
make
./my_app
```

## Available Lie Groups

- **SO2**: 2D rotations
- **SE2**: 2D rigid transformations (rotation + translation)
- **SO3**: 3D rotations
- **SE3**: 3D rigid transformations (rotation + translation)
- **Sim3**: 3D similarity transformations (rotation + translation + scale)
- **ScSO3**: Scaled 3D rotations

## Uninstall

To remove the installed files:

```bash
sudo rm -rf /usr/local/include/sophus
sudo rm /usr/local/lib/libSophus.so
sudo rm -rf /usr/local/share/Sophus
```
