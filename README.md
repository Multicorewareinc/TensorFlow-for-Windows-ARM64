<div align="center">
  <img src="https://www.tensorflow.org/images/tf_logo_horizontal.png">
</div>

# TensorFlow for Windows ARM64 (Unofficial Build)

This repository contains **unofficial prebuilt TensorFlow wheels for Windows on ARM64**.

> [!IMPORTANT]
> These wheels are **not official TensorFlow releases**. They are community-built binaries compiled from the official TensorFlow source code and are **not affiliated with, endorsed by, or supported by Google or the TensorFlow project**.

## Build Information

| Item               | Value                       |
| ------------------ | --------------------------- |
| TensorFlow Version | 2.22.0-dev0+selfbuilt       |
| Platform           | Windows ARM64 (`win_arm64`) |
| Supported Python   | Python 3.13 (ARM64)         |
| Compiler           | LLVM `clang-cl` 22          |
| Build System       | Bazel 7.7.0                 |

## Features

* Native TensorFlow wheel for **Windows ARM64**
* Native **oneDNN v3** support enabled
* **Arm Compute Library (ACL)** accelerated GEMM through oneDNN
* XLA CPU support enabled

---

# Installing Python 3.13 (ARM64)

1. Download the latest **Windows ARM64** installer from the official Python website:

   https://www.python.org/downloads/windows/

2. Run the installer.

   * Enable **Add Python to PATH**.
   * Select **Install Now**.

3. Verify the installation:

```bash
python --version
pip --version
```

Expected output:

```text
Python 3.13.x
```

---

# Installation

## Step 1: Install the TensorFlow wheel

Download the wheel from the repository **Releases** page.

Install it without dependencies:

```bash
pip install tensorflow-2.22.0.dev0+selfbuilt-cp313-cp313-win_arm64.whl --no-deps
```

---

## Step 2: Install the required Python dependencies

```bash
pip install absl-py astunparse flatbuffers gast google_pasta keras-nightly libclang ml_dtypes numpy opt_einsum packaging protobuf requests setuptools six termcolor typing_extensions wrapt
```

---

## Step 3: Install h5py

```bash
pip install --only-binary=:all: h5py
```

---

## Step 4: Install grpcio

Download the Windows ARM64 wheel from:

https://github.com/khmyznikov/PyEnv-WoA-State/releases/download/grpcio-1.84.0-win_arm64/grpcio-1.84.0.dev0-cp313-cp313-win_arm64.whl

Then install it:

```bash
pip install grpcio-1.84.0.dev0-cp313-cp313-win_arm64.whl
```

---

# Verify the Installation

```python
import tensorflow as tf

print(tf.__version__)
print(tf.version.COMPILER_VERSION)
print(tf.config.list_physical_devices())
```

Expected output:

```text
2.22.0-dev0+selfbuilt
MSVC 195136248
[PhysicalDevice(name='/physical_device:CPU:0', device_type='CPU')]
```

To verify that oneDNN is enabled, run TensorFlow with:

```powershell
$env:ONEDNN_VERBOSE=2
$env:TF_ENABLE_ONEDNN_OPTS=1
```

The output should contain entries similar to:

```text
onednn_verbose,v1,info,oneDNN v3.x
onednn_verbose,v1,primitive,exec,cpu,matmul,gemm:acl
```

which indicates that oneDNN is using the **Arm Compute Library (ACL)** backend for optimized CPU operations.

---

# Source Modifications

This build is based on the official TensorFlow source code and includes modifications required to enable native Windows ARM64 support.

Major changes include:

* Added native Windows ARM64 (`win_arm64`) Bazel platform and build configurations.
* Added LLVM `clang-cl` toolchain support for Windows ARM64.
* Added Windows ARM64 support for TensorFlow's legacy `rules_python` (`pip_parse`) dependency resolution.
* Updated platform detection and CPU feature handling for Windows ARM64.
* Added Windows ARM64 support for XLA CPU target machine configuration.
* Updated TensorFlow build rules to recognize and build for Windows ARM64.
* Enabled native oneDNN support on Windows ARM64, including Arm Compute Library (ACL) acceleration.

---

# License

TensorFlow is licensed under the **Apache License 2.0**.

This repository redistributes binaries built from the official TensorFlow source code.

To comply with the Apache License 2.0:

* The original **LICENSE** file from TensorFlow is included in this repository.
* Existing copyright and license notices have been preserved.
* Source-level modifications made for Windows ARM64 support are documented above.

This repository does not intentionally introduce additional third-party components beyond those already included by TensorFlow. Any future additions will include the appropriate license notices.

---

# Disclaimer

This project is an **unofficial community build** of TensorFlow for **Windows ARM64**.

It is **not affiliated with, endorsed by, or supported by Google or the TensorFlow project**. Issues specific to these binaries should be reported in this repository rather than the official TensorFlow project.

