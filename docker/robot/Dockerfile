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
          -D INSTALL_PYTHON_EXAMPLES=OFF \
          -D WITH_TBB=ON 
          -D WITH_OPENMP=ON \
          -D WITH_IPP=ON \
          -D CMAKE_BUILD_TYPE=RELEASE \
          -D WITH_NVCUVID=ON \
          -D WITH_CUDA=ON \
          -D WITH_CSTRIPES=ON \
          -D WITH_OPENCL=ON \
          #-D OPENCV_EXTRA_MODULES_PATH=/opencv_contrib/modules \
          -D BUILD_EXAMPLES=OFF .. && \
    make -j4 && \
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
