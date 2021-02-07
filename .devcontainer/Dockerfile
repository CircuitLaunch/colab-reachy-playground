FROM ubuntu:18.04

RUN apt-get update && apt-get upgrade -y
RUN apt-get install wget screen bzip2 curl -y
RUN apt-get install libpulse-dev libasound2-dev pavucontrol -y
RUN apt-get install -y git git-lfs

RUN groupadd reachy
RUN useradd --create-home --shell /bin/bash reachy --gid reachy
RUN adduser reachy sudo

USER reachy
WORKDIR /home/reachy
SHELL ["/bin/bash", "-c"]

# Anaconda
RUN curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -s -o /tmp/Miniconda3-latest-Linux-x86_64.sh
RUN bash /tmp/Miniconda3-latest-Linux-x86_64.sh -b -p ~/miniconda && rm /tmp/Miniconda3-latest-Linux-x86_64.sh
COPY --chown=reachy:reachy environment.yml /tmp
RUN source /home/reachy/miniconda/bin/activate && conda update -n base conda && conda init && conda env create -f /tmp/environment.yml
RUN rm /tmp/environment.yml