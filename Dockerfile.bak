FROM alpine:3.14

# you can specify python version during image build
ARG PYTHON_VERSION=3.6.1

# install build dependencies and needed tools
RUN apk add \
    wget \
	curl \
    gcc \
    make \
    zlib-dev \
    libffi-dev \
    openssl-dev \
    musl-dev

RUN cd /opt \
    && wget https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz \                                              
    && tar xzf Python-${PYTHON_VERSION}.tgz

RUN cd /opt/Python-${PYTHON_VERSION} \ 
    && ./configure --prefix=/usr --enable-optimizations --with-ensurepip=install \
    && make install \
    && rm /opt/Python-${PYTHON_VERSION}.tgz /opt/Python-${PYTHON_VERSION} -rf

ADD ./requirements.txt /opt/webapp-conntest/

WORKDIR /opt/webapp-conntest

RUN pip install -r requirements.txt

ADD . /opt/webapp-conntest

EXPOSE 8080

ENTRYPOINT ["python", "app.py"]
