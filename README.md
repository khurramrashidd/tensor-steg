# TensorSteg: Neural Weight Steganography

A zero-impact covert channel implementation exploiting the IEEE-754 single-precision floating-point format in deep neural network weights.

## How It Works

A standard `float32` tensor element is structured as:
* 1 Sign bit
* 8 Exponent bits
* 23 Mantissa (fractional) bits

`TensorSteg` casts the weight tensor into raw `uint32` memory layouts via `numpy.view()`. It then embeds arbitrary binary payloads into bit 0 (the least significant bit) of the 23-bit mantissa.

* **Perturbation magnitude:** $\approx 2^{-23} \approx 1.19 \times 10^{-7}$ per parameter.
* **Accuracy impact:** Zero degradation. Predictions pass strict `torch.allclose(atol=1e-6)` checks.
* **Stealth:** Model architecture, checksum-like inspections, and inference routines run unchanged without raising security warnings.

## Usage

```bash
git clone [https://github.com/your-username/tensor-steg.git](https://github.com/your-username/tensor-steg.git)
cd tensor-steg
python tensor_steg.py
