FROM ros:melodic

ENV ROS_DISTRO melodic

RUN mkdir workspace
WORKDIR /workspace

# install ros-melodic-desktop-full
RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-desktop-full \
    && rm -rf /var/lib/apt/lists/*

# install bootstrap tools 
RUN apt-get update && apt-get install --no-install-recommends -y \
    python-rosdep \
    python-rosinstall \
    python-rosinstall-generator \
    python-wstool build-essential \
    && rm -rf /vr/lib/apt/lists/*

# install dependencies for orbslam3
RUN apt-get update && apt-get install gcc g++

# install Pangolin
RUN apt-get update && apt-get install -y \ 
    libglew-dev \
    cmake \
    libboost-dev libboost-thread-dev libboost-filesystem-dev \
    libpython2.7-dev

RUN git clone https://github.com/stevenlovegrove/Pangolin.git \
    && cd Pangolin \
    && mkdir build \
    && cd build \
    && cmake -DCPP11_NO_BOOST=1 .. \
    && make

# install Opencv
RUN apt-get install -y \
    libopencv-dev

# install Eigen
RUN apt-get install -y \
    libeigen3-dev

# install BLAS, LAPACK
RUN apt-get install -y \
    libblas-dev \
    liblapack-dev

RUN git clone https://github.com/UZ-SLAMLab/ORB_SLAM3.git \
    && cd ORB_SLAM3 \
    && chmod +x build.sh \
    && ./build.sh

CMD ["/bin/bash"]
