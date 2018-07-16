FROM duckietown/slimremote-base

RUN [ "cross-build-start" ]

RUN cd opencv && \
    mkdir build && \
    cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
          -D CMAKE_INSTALL_PREFIX=/usr/local \
          -D INSTALL_C_EXAMPLES=OFF \
          -D BUILD_PERF_TESTS=OFF \
          -D BUILD_TESTS=OFF \
          -D INSTALL_TESTS=OFF \
          -D BUILD_opencv_apps=OFF \
          -D BUILD_DOCS=OFF \
          -D BUILD_PNG=OFF \
          -D BUILD_TIFF=OFF \
          -D BUILD_JPEG=OFF \
          -D BUILD_JASPER=OFF \
          -D BUILD_ZLIB=OFF \
          -D BUILD_EXAMPLES=OFF \
          -D BUILD_opencv_java=OFF \
          -D INSTALL_PYTHON_EXAMPLES=OFF \
          -D WITH_TBB=OFF \
          -D BUILD_TBB=OFF \
          -D WITH_OPENMP=ON \
          -D WITH_IPP=ON \
          -D CMAKE_BUILD_TYPE=RELEASE \
          -D WITH_CUDA=OFF \
          -D ENABLE_NEON=ON \
          -D ENABLE_VFPV3=ON \
          -D CMAKE_INSTALL_PREFIX=$(python3 -c "import sys; print(sys.prefix)") \
          -D PYTHON_EXECUTABLE=$(which python3.6) \
          -DPYTHON_INCLUDE_DIR=$(python3 -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
          -DPYTHON_PACKAGES_PATH=$(python3 -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") .. \
          -D BUILD_EXAMPLES=OFF ..
          
RUN cd opencv/build/ && \
    make -j8 && \
    make install && \
    ldconfig
    
# cleanup
RUN rm -rf ~/opencv && \
    rm -rf ~/opencv_contrib && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get remove libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev libavcodec-dev \
    libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev \
    libx264-dev libatlas-base-dev python3-dev

RUN git clone --depth 1 https://github.com/duckietown/duckietown-slimremote.git && \
    cd duckietown-slimremote && \
    pip3 install -e .

RUN [ "cross-build-end" ]

EXPOSE 5558 8902

CMD ["duckietown-start-robot2"]
