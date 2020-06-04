
# build singularity img from dockerfile

https://stackoverflow.com/questions/60314664/how-to-build-singularity-container-from-dockerfile


```
docker build -t local/phylowgs .
# for this step to work, we need a fairly recent version of singularity
# https://github.com/hpcng/singularity/blob/master/INSTALL.md
singularity build phylowgs.sif docker-daemon://local/phylowgs:latest
```


## install singularity:

https://github.com/hpcng/singularity/blob/master/INSTALL.md

```
sudo apt-get update && \
  sudo apt-get install -y build-essential \
  libseccomp-dev pkg-config squashfs-tools cryptsetup

export VERSION=1.13.7 OS=linux ARCH=amd64  # change this as you need

wget -O /tmp/go${VERSION}.${OS}-${ARCH}.tar.gz https://dl.google.com/go/go${VERSION}.${OS}-${ARCH}.tar.gz && \
  sudo tar -C /usr/local -xzf /tmp/go${VERSION}.${OS}-${ARCH}.tar.gz

echo 'export GOPATH=${HOME}/go' >> ~/.bashrc && \
  echo 'export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin' >> ~/.bashrc && \
  source ~/.bashrc
  
mkdir -p ${GOPATH}/src/github.com/sylabs && \
  cd ${GOPATH}/src/github.com/sylabs && \
  git clone https://github.com/sylabs/singularity.git && \
  cd singularity
# To build a stable version of Singularity, check out a release tag before compiling:

git checkout v3.6.0
# Compiling Singularity
# You can build Singularity using the following commands:

cd ${GOPATH}/src/github.com/sylabs/singularity && \
  ./mconfig && \
  cd ./builddir && \
  make && \
  sudo make install
# And that's it! Now you can check your Singularity version by running:

singularity version

```
