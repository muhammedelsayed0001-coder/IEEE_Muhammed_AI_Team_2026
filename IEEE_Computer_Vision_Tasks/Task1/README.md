# Image Filtering Assignment

A from-scratch NumPy implementation of 2D image convolution, used to build box blur, Gaussian blur, Sobel, Laplacian, and Derivative-of-Gaussian (DoG) filters. Results are checked against OpenCV's built-in equivalents.

## Contents

| File | Description |
|---|---|
| `assignment1_image_filtering.ipynb` | Full solution as an executed Jupyter notebook (recommended submission file) |
| `report.pdf` | 4-page write-up with figures, results, and explanations |
| `run_log.txt` | Captured console output from the standalone script run |
| `test_image.webp` | Test image used throughout (900×600 brick wall photo) |
| `figures/` | Generated output images referenced in the report/notebook |

## What this covers

`my_conv` is written with NumPy only, no `cv2`/`scipy` filtering calls, and follows a no-flip convolution convention. It's vectorized with sliding-window views so it runs at full image resolution in reasonable time.

Box and Gaussian kernels are built from their mathematical formulas and normalized to sum to 1, with kernel size validated as odd. Sobel and Laplacian give the derivative filters; a Derivative-of-Gaussian (DoG) filter folds smoothing and differentiation into a single step.

Edge detection runs on the test image, and a noise-robustness experiment compares Gaussian-then-Sobel against direct DoG filtering. Everything is checked against OpenCV (`cv2.filter2D`, `cv2.getGaussianKernel`); differences come out around 1e-15, well under the 1e-9 threshold required.

## Requirements

- Python 3.12+
- NumPy
- OpenCV (`opencv-python`)
- Matplotlib
- Jupyter (to run the `.ipynb`)

Exact versions used are logged in `run_log.txt`.

## Running

```bash
jupyter notebook assignment1_image_filtering.ipynb
```

or, for the standalone script version:

```bash
python assignment1_image_filtering.py
```

## Notes

The assignment allows submitting a single `.py` or `.ipynb` file. Submit the notebook: it includes inline figures and markdown explanations the script doesn't.

The noise experiment compares outputs with Pearson correlation instead of raw difference. Sobel (unnormalized finite-difference) and DoG (normalized Gaussian derivative) differ by a scale/sign factor by construction, not because either is wrong.
