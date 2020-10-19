FROM fedora:latest
RUN yum update -y && yum install -y root root-montecarlo-eg cmake3 make git wget gmp-devel gcc-gfortran
RUN git clone https://gitlab.cern.ch/hepmc/HepMC.git
RUN mkdir hepmc-build && \ 
    cd hepmc-build && \
    cmake3 -DCMAKE_INSTALL_PREFIX=/hepmc-install -Dmomentum=GEV -Dlength=MM -Dbuild_docs:BOOL=OFF /HepMC && \
    make -j$(nproc) install && \
    cd / && \
    rm -fr HepMC hepmc-build
ENV HEPMC_ROOT="/hepmc-install"
RUN wget http://fastjet.fr/repo/fastjet-3.3.4.tar.gz && \
    tar zxvf fastjet-3.3.4.tar.gz && \
    cd fastjet-3.3.4/ && \
    ./configure --prefix=/fastjet-install && \
    make -j$(nproc) && \
    make install && \
    cd / && \
    rm -fr fastjet-3.3.4.tar.gz fastjet-3.3.4
ENV PATH=$PATH:/fastjet-install/bin
ENV FASTJET="/fastjet-install"
RUN wget http://fastjet.hepforge.org/contrib/downloads/fjcontrib-1.045.tar.gz && \
    tar zxvf fjcontrib-1.045.tar.gz && \
    cd fjcontrib-1.045 && \
    ./configure && \
    make -j$(nproc) && \
    make install && \
    make fragile-shared -j$(nproc) && \
    make fragile-shared-install && \
    cd / && \
    rm -fr fjcontrib-1.045.tar.gz fjcontrib-1.045
ENV LD_LIBRARY_PATH=/lib:/lib64:$LD_LIBRARY_PATH