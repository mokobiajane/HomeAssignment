
# 🖼️ Parallel BMP Image Processor

**Author**: Mokobia Jane Chidima  
**Group**: 24.B83-mm  
**Email**: st135735@student.spbu.ru  
**Date**: June 2025  

---

## 📋 Overview

This project implements a multithreaded C++ program for processing BMP (Bitmap) images. It performs the following operations efficiently using **parallelism**:

- Grayscale conversion  
- Clockwise and counterclockwise image rotation  
- Gaussian blur filtering  

The goal is to reduce computation time for large images using `std::thread` and modern C++17 features.

---

## 📚 Doxygen Documentation

To generate the documentation:

```bash
doxygen Doxyfile
xdg-open docs/html/index.html
```

- HTML output is stored in `docs/html/index.html`  
- Uses `include/` and `src/` as input directories  

---

## 🛠️ Build Instructions

### 1. Requirements

- C++17 compiler (e.g., `g++`)  
- `make`  
- `doxygen` (for documentation)  

### 2. Build & Run


```bash
make         # Compile
./lab        # Run the program
doxygen Doxyfile && xdg-open docs/html/index.html   # Generate Doxygen docs
make clean   # Clean build artifacts
```

---


## 🏗️ Project Structure

```
parallel-bmp/
├── include/
│   └── main.h                # Function declarations, structs
├── src/
│   └── main.cpp & test.cpp            # Image processing logic and entry p
├── images/
│   └── input_image.bmp       # Source image for testing, generated images
|               
├── docs/                     # Auto-generated Doxygen documentation
├── Doxyfile                  # Doxygen configuration
├── Makefile                  # Build script with doc generation
└── .github/
    └── workflows/
        └── ci.yml            # GitHub Actions CI config
```

---

## ⚙️ Implementation Details

### ✅ Multithreading Utility

```cpp
template <typename Func>
void parallel_for(int start, int end, int num_threads, Func func);
```

Distributes image rows across available threads for concurrent processing. Uses `std::thread` and `hardware_concurrency()`.

---

### ✅ Grayscale Conversion

Each pixel is converted using the formula:

```cpp
gray = 0.3 * R + 0.59 * G + 0.11 * B
```

This conversion is done in parallel for each row.

---

### ✅ Rotation Algorithms

- **Clockwise rotation**:  
  Rotates the image by 90° using a transpose and flip strategy.

- **Counterclockwise rotation**:  
  Performs a similar operation in reverse.

Both are parallelized across rows.

---

### ✅ Gaussian Blur Filtering

Applies a 5×5 Gaussian kernel:

```
[ 1  4  7  4  1 ]
[ 4 16 26 16  4 ]
[ 7 26 41 26  7 ]
[ 4 16 26 16  4 ]
[ 1  4  7  4  1 ]
```

- Applied to interior pixels in parallel  
- Edges are handled separately (non-parallel)

---

## 🧪 Performance Metrics

Measured using `std::chrono::high_resolution_clock`:

| Operation           | Time (ms) | Notes                  |
|--------------------|-----------|------------------------|
| Grayscale           | ~50–100   | Depends on resolution  |
| Clockwise rotation  | ~40–80    |                        |
| Counterclockwise    | ~40–80    |                        |
| Gaussian filter     | ~100–200  | Heaviest operation     |

---

## 📁 Input and Output

- Input BMP image: `images/input_image.bmp`  
- Output files:  
  - `output_clockwise.bmp`  
  - `output_counterclockwise.bmp`  
  - `output_filtered.bmp`

All output images are saved in grayscale, 8-bit indexed BMP format.

---

## 🧼 Memory Usage

Memory allocation is tracked for the grayscale image. The raw pixel memory usage is:

```
width × height bytes (1 byte per pixel)
```

E.g., for a 1024×768 image:

```
1024 × 768 = 786,432 bytes ≈ 768 KB
```

---

## 🧪 Continuous Integration (CI)

A **GitHub Actions** workflow (`.github/workflows/ci.yml`) is included to:

- Compile the project  
- Generate Doxygen documentation  
- Ensure build integrity on each push or pull request  

---


## ✅ Summary

This project demonstrates how to:

- Work with raw BMP file formats  
- Implement image transformations  
- Use `std::thread` for parallelism  
- Track performance and memory  
- Apply software engineering practices (CI, docs, modular code)  

It is designed to be **fast**, **modular**, and **extendable** for future image processing features.

