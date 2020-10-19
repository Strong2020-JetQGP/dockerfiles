FROM sl:7
RUN yum update -y
RUN yum install -y wget make gcc gcc-c++ gcc-gfortran compat-gcc-44-gfortran
RUN wget https://lhapdf.hepforge.org/downloads?f=old/lhapdf-5.9.1.tar.gz -O lhapdf-5.9.1.tar.gz && tar -xvzf lhapdf-5.9.1.tar.gz && rm lhapdf-5.9.1.tar.gz
RUN wget https://jewel.hepforge.org/downloads/?f=jewel-2.2.0.tar.gz -O jewel-2.2.0.tar.gz && tar -xvzf jewel-2.2.0.tar.gz && rm jewel-2.2.0.tar.gz
WORKDIR "/lhapdf-5.9.1"
RUN ./configure && \
    make && \
    make install && \
    mkdir /usr/local/share/lhapdf/PDFsets  && \
    wget https://lhapdf.hepforge.org/downloads?f=pdfsets/5.9.1/cteq6ll.LHpdf -O /usr/local/share/lhapdf/PDFsets/cteq6ll.LHpdf  && \
    wget https://lhapdf.hepforge.org/downloads?f=pdfsets/5.9.1/EPS09LOR_208.LHgrid -O /usr/local/share/lhapdf/PDFsets/EPS09LOR_208.LHgrid 
WORKDIR "/jewel-2.2.0"
RUN sed -i 's+/home/lhapdf/install/lib/+/usr/local/lib/+g' Makefile
RUN make
ENV LD_LIBRARY_PATH=/usr/local/lib/:$LD_LIBRARY_PATH
ENV LHAPATH=/usr/local/share/lhapdf/PDFsets
ENV PATH="/jewel-2.2.0:${PATH}"
WORKDIR "/work"
CMD [ "jewel-2.2.0-vac" ]