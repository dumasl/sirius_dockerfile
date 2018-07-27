FROM ldumas/python_gdal_dockerfile:py_gdal

##
# install FFTW & doxygen
RUN . restart_env && yum install -y fftw3-devel doxygen

##
# set GDAL_DIR for cmake configuration
ENV GDAL_DIR=${OPT_GDAL_DIR}

##
# env latex if doxygen with latex

RUN . restart_env && yum install -y fontconfig freetype freetype-devel fontconfig-devel perl-Digest-MD5 dvipng

RUN . restart_env && wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz; \
	mkdir /install-tl-unx; \
	tar -xvf install-tl-unx.tar.gz -C /install-tl-unx --strip-components=1; \
    echo "selected_scheme scheme-basic" >> /install-tl-unx/texlive.profile; \
    echo "TEXDIR /usr/local/texlive/current/" >> /install-tl-unx/texlive.profile; \
	/install-tl-unx/install-tl -profile /install-tl-unx/texlive.profile; \
    rm -r /install-tl-unx; \
    rm install-tl-unx.tar.gz

ENV PATH=/usr/local/texlive/current/bin/x86_64-linux:${PATH}

RUN tlmgr install latexmk && tlmgr install ucs && tlmgr install algorithms && tlmgr install anyfontsize

RUN tlmgr install float 
RUN tlmgr install xcolor xtab 
RUN tlmgr install multirow 
RUN tlmgr install collection-fontsrecommended 
RUN tlmgr install sectsty
RUN tlmgr install tocloft
RUN tlmgr install epstopdf
