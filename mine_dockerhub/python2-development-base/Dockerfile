# python-development-base

FROM tiagoprn/python2-base:v0.1

MAINTAINER Tiago Paranhos Lima (tiago@tiagoprnl.me)

USER root

RUN yum update -y ; yum clean all 

WORKDIR /build

# Requirement to use "monary" (mongodb c driver python wrapper)
RUN printf 'Installing libbson...[WAIT]'
RUN git clone git://github.com/mongodb/libbson.git
RUN cd libbson && ./autogen.sh && make && make install && cd ..
RUN printf 'Installing libbson...[DONE]'

# Requirement to use "monary" (mongodb c driver python wrapper)
RUN printf 'Installing mongo-c-driver...[WAIT]'
RUN git clone https://github.com/mongodb/mongo-c-driver.git
RUN cd mongo-c-driver && ./autogen.sh && make && make install && cd .. 
RUN printf 'Installing mongo-c-driver...[DONE]'

RUN pip install pymongo motor

RUN pip install cryptography pyopenssl ndg-httpsclient pyasn1

RUN pip install urllib3[secure]

RUN pip install pkgconfig

RUN pip install cython

RUN pip install gevent

# Install ipython for jupyter notebooks support 
RUN pip install -U "ipython[all]"
RUN pip install ipywidgets

# Install your specific project requirements:
ADD requirements* /build/

# Install your specific python project requirements...
RUN printf 'python requirements...[WAIT]'
RUN pip install -r requirements.txt
RUN printf 'python requirements...[DONE]'

USER appuser

WORKDIR /code

