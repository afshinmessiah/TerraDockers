# adapted from https://hub.docker.com/r/jupyter/base-notebook/ AKA https://github.com/jupyter/docker-stacks/tree/master/base-notebook

# FROM marketplace.gcr.io/google/ubuntu1804:latest
FROM gcr.io/gcp-runtimes/ubuntu_18_0_4:latest
USER root

#######################
# Prerequisites
#######################
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -yq --no-install-recommends \

    # gnupg requirement
    dirmngr \
    gnupg \

    # curl requirement
    ca-certificates \
    curl \

    # google-cloud-sdk requirement
    lsb-release \
    gcc-6 \
    gcc-8 \

    # useful utilities for debugging within the docker
    unzip \
    nano \
    vim \
    procps \

    # python requirements
    checkinstall \
    build-essential \
    zlib1g-dev \

    # pip requirements
    libssl1.0-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    llvm \
    libncurses5-dev \
    libncursesw5-dev \
    tk-dev \
    libffi-dev \
    liblzma-dev \
    python-openssl \

    # install script requirements
    sudo \
    wget \
    locales \
    git \
    jq \

    # for ssh-agent and ssh-add
    keychain \



 # Uncomment en_US.UTF-8 for inclusion in generation
 && sed -i 's/^# *\(en_US.UTF-8\)/\1/' /etc/locale.gen \
 # Generate locale
 && locale-gen \

 # google-cloud-sdk separately because it need lsb-release and other prereqs installed above
 && export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" \
 && echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" > /etc/apt/sources.list.d/google-cloud-sdk.list \
 && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
 && apt-get update \
 && apt-get install -yq --no-install-recommends \
    google-cloud-sdk \

 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# # Python3, kernel, and pip
RUN apt update \
   && apt install -yq software-properties-common \
   && add-apt-repository ppa:deadsnakes/ppa \
   && apt install -yq python3.7 \
   && update-alternatives --install /usr/local/bin/python3 python3 /usr/bin/python3.7 1 \
   && apt-get -yq install python3-pip \
   && /usr/local/bin/python3 -m pip install --upgrade pip

RUN apt-get update && apt-get install -yq --no-install-recommends plastimatch \
&& pip3 install google-cloud-bigquery \
&& pip3 install SimpleITK \
&& pip3 install pydicom \
&& pip3 install matplotlib \
&& pip3 install seaborn \
&& pip3 install pandas \
&& pip3 install numpy \
&& pip3 install sklearn
USER $USER


