FROM python:3.10-slim
RUN apt update --no-install-recommends -y && apt install wget -y && apt clean -y

# Install java
ENV JAVA_HOME /usr/local/jre1.8.0_333
ENV PATH $JAVA_HOME/bin:$PATH

RUN wget --progress=dot:giga -O jre1.8.0_333.tar.gz "https://sdlc-esd.oracle.com/ESD6/JSCDL/jdk/8u333-b02/2dee051a5d0647d5be72a7c0abff270e/jre-8u333-linux-x64.tar.gz?GroupName=JSC&FilePath=/ESD6/JSCDL/jdk/8u333-b02/2dee051a5d0647d5be72a7c0abff270e/jre-8u333-linux-x64.tar.gz&BHost=javadl.sun.com&File=jre-8u333-linux-x64.tar.gz&AuthParam=1653147798_aa359b9623f89b351fde58aecd0b81e8&ext=.gz"; \
	\
	mkdir -p "$JAVA_HOME"; \
	\
	tar --extract \
		--file jre1.8.0_333.tar.gz \
		--directory "$JAVA_HOME" \
		--strip-components 1 \
		--no-same-owner \
	; \ 
	rm jre1.8.0_333.tar.gz*; \
	\
	rm -rf /var/lib/apt/lists/*; \
	\
	apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false;


RUN python -m pip install --upgrade pip

RUN pip install --no-cache-dir pyspark notebook requests


# create directory for notebooks
RUN mkdir /notebooks

EXPOSE 4040 8888

# start the jupyter notebook in server mode
CMD ["jupyter","notebook","--ip=0.0.0.0","--port=8888","--no-browser","--allow-root", "--notebook-dir=/notebooks"]

# docker build --rm -t pyspark . && docker run --rm --name pyspark -v $(pwd)/data:/notebooks -p 4040:4040 -p 8888:8888 pyspark