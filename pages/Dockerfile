FROM ldumas/python_gdal_dockerfile:py_gdal

##
# env sphinx
RUN . /usr/bin/pygdal_env && pip install sphinx

RUN . /usr/bin/pygdal_env && pip install sphinx_rtd_theme

RUN . /usr/bin/pygdal_env && pip install pillow

RUN . /usr/bin/pygdal_env && pip install sphinx-autoapi

RUN . /usr/bin/pygdal_env && pip install ipython

##
# env latex for sphinx

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

RUN tlmgr install latexmk 
RUN tlmgr install ucs 
RUN tlmgr install algorithms 
RUN tlmgr install anyfontsize

