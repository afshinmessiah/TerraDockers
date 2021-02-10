FROM tensorflow/tensorflow:1.15.4-gpu-py3

LABEL maintainer="dennis_bontempi@dfci.harvard.edu"
LABEL version="1.0"
LABEL description="Terra Docker for Deep Prognosis."

RUN apt-get update && apt-get install --no-install-recommends --no-install-suggests -y curl
RUN apt-get install -y unzip
RUN apt-get install -y plastimatch

ENV USER terra-test
ENV UID 1000
RUN useradd -m -s /bin/bash -N -u $UID $USER

ENV HOME /home/$USER

RUN mkdir /home/$USER/src
RUN mkdir /home/$USER/data
RUN mkdir /home/$USER/models

COPY src $HOME/src
COPY data $HOME/data
COPY models $HOME/models  
COPY requirements.txt $HOME
COPY run_pipeline.sh $HOME

RUN pip3 install -r $HOME/requirements.txt

ENTRYPOINT ["/bin/bash"]
