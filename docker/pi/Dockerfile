FROM elswork/rpi-tensorflow:1.7.0

RUN apt-get update -y

RUN apt install -y curl \
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

# OpenCV
ENV OPENCV_VERSION="3.4.1"
ENV OPENCV_DIR="/opt/opencv/"

ADD https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.tar.gz ${OPENCV_DIR}

RUN cd ${OPENCV_DIR} && \
    tar -xzf ${OPENCV_VERSION}.tar.gz && \
    rm ${OPENCV_VERSION}.tar.gz && \
    mkdir ${OPENCV_DIR}opencv-${OPENCV_VERSION}/build && \
    cd ${OPENCV_DIR}opencv-${OPENCV_VERSION}/build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local .. && make -j4 && make install && \
    mv /usr/local/lib/python3.4/dist-packages/cv2.cpython-34m.so /usr/local/lib/python3.4/dist-packages/cv2.so && \
    rm -rf ${OPENCV_DIR}

WORKDIR /

RUN mkdir /facematch

RUN chown -R root:root /facematch

RUN chmod 755 /facematch

WORKDIR /facematch

RUN pip3 install absl-py==0.1.10 \
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

