# stretch because that's the same as the hypriotOS image
FROM  resin/rpi-raspbian:stretch

RUN [ "cross-build-start" ]

# build deps
RUN apt-get update && \
    apt-get install --no-install-recommends -y build-essential git wget cmake pkg-config \
    libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev libavcodec-dev \
    libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev \
    libx264-dev libatlas-base-dev gfortran python3-dev

RUN wget https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py && \
    rm get-pip.py

ADD https://github.com/opencv/opencv/archive/3.4.1.tar.gz opencv.tar.gz
RUN tar -xvzf opencv.tar.gz && mv opencv-3.4.1 opencv

#ADD https://github.com/opencv/opencv_contrib/archive/3.4.1.tar.gz opencv_contrib.tar.gz
#RUN tar -xvzf opencv_contrib.tar.gz && mv opencv_contrib-3.4.1 opencv_contrib

RUN [ "cross-build-end" ]
