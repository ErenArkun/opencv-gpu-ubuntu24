# OpenCV GPU Destekli Derleme Rehberi – Ubuntu 24.04

## Türkçe Açıklama

Bu rehber, **Ubuntu 24.04** üzerinde **Python 3.12**, **CUDA 12.6** ve **cuDNN 9.8** ile GPU destekli **OpenCV** kurulumu için adım adım bir rehber sunar.

---

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/3/32/OpenCV_Logo_with_text_svg_version.svg" alt="OpenCV Logo" width="250"/>
  &nbsp;&nbsp;&nbsp;
  <img src="https://assets.ubuntu.com/v1/29985a98-ubuntu-logo32.png" alt="Ubuntu Logo" width="150"/>
</p>

---

### ⚠️ Önemli Uyum Bilgileri

- **Python 3.12** ve **Ubuntu 24.04** ile varsayılan olarak gelir.
- **cuDNN 9.8**, yalnızca **CUDA 12.6** ve üzeri sürümlerle uyumludur. Daha eski CUDA sürümleriyle **uyumsuzdur**.
- Derleme işlemlerinde hata almamak için sistem kitaplıklarının ve sürümlerinin doğru şekilde seçilmesi gerekir.

---

### Gerekli Dosyalar

- **CUDA 12.6**: [CUDA 12.6 İndirme Sayfası](https://developer.nvidia.com/cuda-12-6-0-download-archive)
- **cuDNN 9.8.0**: [cuDNN 9.8 İndirme Sayfası](https://developer.nvidia.com/cudnn-downloads)
- **OpenCV 4.11**: [OpenCV 4.11 Sürümü](https://opencv.org/releases/)
- **OpenCV 4.11 Contrib Kütüphaneleri**: [OpenCV Contrib Kütüphaneleri 4.11.0](https://github.com/opencv/opencv_contrib/tree/4.11.0)

---

### ⚙️ CMake Komutu

OpenCV'yi GPU desteğiyle derlemek için kullanılan CMake komutu, `cmake_command.txt` dosyasında bulunmaktadır. Sisteminize uygun komutları buraya eklemeyi unutmayın.

---

### 📋 Derleme Adımları

1. Sistemi güncelleyin:
    ```bash
    sudo apt update
    ```

2. `cmake komutu` openCV derleyin:
    ```bash
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D INSTALL_C_EXAMPLES=ON \
      -D INSTALL_PYTHON_EXAMPLES=OFF \
      -D WITH_TBB=ON \
      -D WITH_CUDA=ON \
      -D BUILD_opencv_cudacodec=ON \
      -D ENABLE_FAST_MATH=ON \
      -D CUDA_FAST_MATH=ON \
      -D WITH_CUBLAS=ON \
      -D BUILD_opencv_java=OFF \
      -D BUILD_ZLIB=ON \
      -D BUILD_TIFF=ON \
      -D WITH_GTK=ON \
      -D WITH_NVCUVID=ON \
      -D WITH_FFMPEG=ON \
      -D WITH_1394=ON \
      -D OPENCV_GENERATE_PKGCONFIG=ON \
      -D OPENCV_PC_FILE_NAME=opencv4.pc \
      -D OPENCV_ENABLE_NONFREE=ON \
      -D WITH_GSTREAMER=ON \
      -D WITH_V4L=ON \
      -D WITH_QT=ON \
      -D WITH_CUDNN=ON \
      -D OPENCV_DNN_CUDA=ON \
      -D OPENCV_EXTRA_MODULES_PATH=../opencv_contrib-4.11.0/modules \
      -D BUILD_EXAMPLES=ON \
      -D PYTHON3_EXECUTABLE=$(which python3) \
      -D PYTHON3_INCLUDE_DIR=$(python3 -c "import sysconfig; print(sysconfig.get_paths()['include'])") \
      -D PYTHON3_LIBRARY=$(python3 -c "import sysconfig; print(sysconfig.get_config_var('LIBDIR') + '/libpython' + sysconfig.get_config_var('VERSION') + '.so')") \
      -D PYTHON3_PACKAGES_PATH=$(python3 -c "import sysconfig; print(sysconfig.get_paths()['purelib'])") \
      -D BUILD_opencv_python3=ON \
      -D OPENCV_PYTHON3_INSTALL_PATH=$(python3 -c "import sysconfig; print(sysconfig.get_paths()['purelib'])") \
      ../opencv-4.11.0
    ```

3. Derlemeyi başlatın:
    ```bash
    make -j$(nproc)
    ```

4. OpenCV'yi kurun:
    ```bash
    sudo make install
    ```

---

### 🔍 OpenCV Kurulumunu Kontrol Etmek

Kurulumun doğru şekilde yapıldığını kontrol etmek için aşağıdaki komutu çalıştırabilirsiniz:
```bash
pkg-config --modversion opencv4
```

# OpenCV GPU Support Compilation Guide – Ubuntu 24.04

## English Explanation

This guide provides a step-by-step process for setting up GPU-supported **OpenCV** on **Ubuntu 24.04** with **Python 3.12**, **CUDA 12.6**, and **cuDNN 9.8**.

---

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/3/32/OpenCV_Logo_with_text_svg_version.svg" alt="OpenCV Logo" width="250"/>
  &nbsp;&nbsp;&nbsp;
  <img src="https://assets.ubuntu.com/v1/29985a98-ubuntu-logo32.png" alt="Ubuntu Logo" width="150"/>
</p>

---

### ⚠️ Important Compatibility Information

- **Python 3.12** and **Ubuntu 24.04** come by default.
- **cuDNN 9.8** is only compatible with **CUDA 12.6** and above. It is **incompatible** with older versions of CUDA.
- It is important to select the correct system libraries and versions to avoid errors during the compilation process.

---

### Required Files

- **CUDA 12.6**: [CUDA 12.6 Download Page](https://developer.nvidia.com/cuda-12-6-0-download-archive)
- **cuDNN 9.8.0**: [cuDNN 9.8 Download Page](https://developer.nvidia.com/cudnn-downloads)
- **OpenCV 4.11**: [OpenCV 4.11 Release](https://opencv.org/releases/)
- **OpenCV 4.11 Contrib Libraries**: [OpenCV Contrib Libraries 4.11.0](https://github.com/opencv/opencv_contrib/tree/4.11.0)

---

### ⚙️ CMake Command

The CMake command used for compiling OpenCV with GPU support is available in the `cmake_command.txt` file. Make sure to add the necessary commands based on your system configuration.

---

### 📋 Compilation Steps

1. Update the system:
    ```bash
    sudo apt update
    ```

2. "Compile OpenCV with the `cmake command`:"
    ```bash
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D INSTALL_C_EXAMPLES=ON \
      -D INSTALL_PYTHON_EXAMPLES=OFF \
      -D WITH_TBB=ON \
      -D WITH_CUDA=ON \
      -D BUILD_opencv_cudacodec=ON \
      -D ENABLE_FAST_MATH=ON \
      -D CUDA_FAST_MATH=ON \
      -D WITH_CUBLAS=ON \
      -D BUILD_opencv_java=OFF \
      -D BUILD_ZLIB=ON \
      -D BUILD_TIFF=ON \
      -D WITH_GTK=ON \
      -D WITH_NVCUVID=ON \
      -D WITH_FFMPEG=ON \
      -D WITH_1394=ON \
      -D OPENCV_GENERATE_PKGCONFIG=ON \
      -D OPENCV_PC_FILE_NAME=opencv4.pc \
      -D OPENCV_ENABLE_NONFREE=ON \
      -D WITH_GSTREAMER=ON \
      -D WITH_V4L=ON \
      -D WITH_QT=ON \
      -D WITH_CUDNN=ON \
      -D OPENCV_DNN_CUDA=ON \
      -D OPENCV_EXTRA_MODULES_PATH=../opencv_contrib-4.11.0/modules \
      -D BUILD_EXAMPLES=ON \
      -D PYTHON3_EXECUTABLE=$(which python3) \
      -D PYTHON3_INCLUDE_DIR=$(python3 -c "import sysconfig; print(sysconfig.get_paths()['include'])") \
      -D PYTHON3_LIBRARY=$(python3 -c "import sysconfig; print(sysconfig.get_config_var('LIBDIR') + '/libpython' + sysconfig.get_config_var('VERSION') + '.so')") \
      -D PYTHON3_PACKAGES_PATH=$(python3 -c "import sysconfig; print(sysconfig.get_paths()['purelib'])") \
      -D BUILD_opencv_python3=ON \
      -D OPENCV_PYTHON3_INSTALL_PATH=$(python3 -c "import sysconfig; print(sysconfig.get_paths()['purelib'])") \
      ../opencv-4.11.0
    ```

3. Start the compilation:
    ```bash
    make -j$(nproc)
    ```

4. Install OpenCV:
    ```bash
    sudo make install
    ```

---

### 🔍 Verify OpenCV Installation

To verify that OpenCV has been installed correctly, run the following command:
```bash
pkg-config --modversion opencv4


