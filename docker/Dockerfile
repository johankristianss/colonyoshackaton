FROM docker.io/tensorflow/tensorflow:2.13.0-gpu

USER root

# Install dependencies
RUN apt-get update && DEBIAN_FRONTEND="noninteractive" TZ="Europe/Stockholm" apt-get install -y python3 python3-pip wget vim git fish libgl1-mesa-glx libglib2.0-0
RUN python3 -m pip install --upgrade pip
RUN pip3 install pycolonies opencv-python tqdm Pillow scikit-learn keras matplotlib numpy

# Install Colonies
ENV PATH="$PATH:/root/go/bin" 
RUN cd /root; wget https://go.dev/dl/go1.20.7.linux-amd64.tar.gz; tar -xzf go1.20.7.linux-amd64.tar.gz;git clone https://github.com/colonyos/colonies.git; cd colonies; make; make install; cd ..; rm -rf go; rm -rf colonies; rm go1.20.7.linux-amd64.tar.gz
RUN mkdir -p /root/.config/fish/

# Post install
COPY ./post_install.sh /bin/post_install.sh
RUN /bin/post_install.sh

# Change shell to fish
SHELL ["fish", "--command"]
RUN chsh -s /usr/bin/fish
ENV SHELL /usr/bin/fish
