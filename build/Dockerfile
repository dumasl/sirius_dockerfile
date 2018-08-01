FROM ldumas/python_gdal_dockerfile:py_gdal

##
# install FFTW & doxygen
RUN . restart_env && yum install -y fftw3-devel

## 
# install doxygen
ENV DOXYGEN_VERSION=1.8.14

RUN . restart_env && yum install -y flex bison

RUN wget http://ftp.stack.nl/pub/users/dimitri/doxygen-${DOXYGEN_VERSION}.src.tar.gz -O /tmp/doxygen-${DOXYGEN_VERSION}.tar.gz && \
    tar -xzvf /tmp/doxygen-${DOXYGEN_VERSION}.tar.gz -C /tmp && \
    cd /tmp/doxygen-${DOXYGEN_VERSION} && \
    mkdir -v build && cd build && cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr -Wno-dev .. && \
    make && make install && \
    rm -rf /tmp/doxygen-${DOXYGEN_VERSION} /tmp/doxygen-${DOXYGEN_VERSION}.tar.gz

##
# set GDAL_DIR for cmake configuration
ENV GDAL_DIR=${OPT_GDAL_DIR}

##
# env latex if doxygen with latex
#
#RUN . restart_env && yum install -y fontconfig freetype freetype-devel fontconfig-devel perl-Digest-MD5 dvipng
#
#RUN . restart_env && wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz; \
#	mkdir /install-tl-unx; \
#	tar -xvf install-tl-unx.tar.gz -C /install-tl-unx --strip-components=1; \
#    echo "selected_scheme scheme-basic" >> /install-tl-unx/texlive.profile; \
#    echo "TEXDIR /usr/local/texlive/current/" >> /install-tl-unx/texlive.profile; \
#	/install-tl-unx/install-tl -profile /install-tl-unx/texlive.profile; \
#    rm -r /install-tl-unx; \
#    rm install-tl-unx.tar.gz
#
#ENV PATH=/usr/local/texlive/current/bin/x86_64-linux:${PATH}
#
#RUN tlmgr install latexmk && tlmgr install ucs && tlmgr install algorithms && tlmgr install anyfontsize
#RUN tlmgr install float 
#RUN tlmgr install xcolor xtab 
#RUN tlmgr install multirow 
#RUN tlmgr install collection-fontsrecommended 
#RUN tlmgr install sectsty
#RUN tlmgr install tocloft
#RUN tlmgr install epstopdf

##
# install git to get back sources
#RUN mkdir /tmp/SOURCES

#COPY $SOURCES_DIR /tmp/SOURCES/

#RUN source /opt/rh/devtoolset-6/enable && cd /tmp/SOURCES/ && mkdir .build && cd .build && cmake3 .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/opt/sirius -DENABLE_CACHE_OPTIMIZATION=ON -DENABLE_GSL_CONTRACTS=OFF -DENABLE_LOGS=ON -DENABLE_UNIT_TESTS=OFF -DENABLE_DOCUMENTATION=ON && make && make install

#RUN rm -rf /tmp/SOURCES
