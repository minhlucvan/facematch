FROM elswork/rpi-tensorflow:1.7.0

RUN apt-get update -y

RUN apt install -y  build-essential \
                    cmake \
                    pkg-config \
                    unzip wget \
                    curl \
                    libjpeg-dev \
                    libtiff5-dev \
                    libjasper-dev \
                    libpng12-dev \
                    libavcodec-dev \
                    libavformat-dev \
                    libswscale-dev \
                    libv4l-dev \
                    libxvidcore-dev \
                    libx264-dev \
                    libgtk2.0-dev \
                    libatlas-base-dev \
                    gfortran \
                    python2.7-dev \
                    python3-dev \
                    python-pip \
                    python-numpy \
                    libsm6 \
                    libxext6 \
                    libxrender1 \
                    libfontconfig1

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

RUN python get-pip.py

RUN apt-get install -y python3-pip

RUN pip install --upgrade pip

RUN python -m pip install -U pip

RUN pip3 install -U pip

RUN pip install absl-py==0.1.10 \
                astroid==1.6.1 \
                bleach==1.5.0 \
                html5lib==0.9999999 \
                imutils==0.4.5 \
                isort==4.3.3 \
                lazy-object-proxy==1.3.1 \
                Markdown==2.6.11 \
                mccabe==0.6.1 \
                numpy==1.14.0 \
                protobuf==3.5.1 \
                pylint==1.8.2 \
                scikit-learn==0.19.1 \
                scipy==1.0.0 \
                six==1.11.0 \
                sklearn==0.0 \
                tensorflow==1.5.0 \
                tensorflow-tensorboard==1.5.1 \
                Werkzeug==0.14.1 \
                wrapt==1.10.11


# OpenCV
ENV OPENCV_VERSION 3.4.1

# download latest source & contrib
RUN cd /tmp && \
    wget -O opencv.zip https://github.com/opencv/opencv/archive/$OPENCV_VERSION.zip && \
    unzip opencv.zip

RUN cd /tmp && \
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/$OPENCV_VERSION.zip && \
    unzip opencv_contrib.zip

# build opencv
RUN cd /tmp/opencv-$OPENCV_VERSION && \
    mkdir build && \
    cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_C_EXAMPLES=ON \
    -D BUILD_PYTHON_SUPPORT=ON \
    -D BUILD_NEW_PYTHON_SUPPORT=ON \
    -D INSTALL_PYTHON_EXAMPLES=ON \
        -D OPENCV_EXTRA_MODULES_PATH=/tmp/opencv_contrib-$OPENCV_VERSION/modules \
    -D BUILD_EXAMPLES=ON .. && \
    make -j4 && \
    make && \
    make install && \
    make clean

# cleanup source
RUN cd /tmp && rm -rf opencv-$OPENCV_VERSION


# facefatch
WORKDIR /

RUN mkdir /facematch

RUN chown -R root:root /facematch

RUN chmod 755 /facematch

WORKDIR /facematch
