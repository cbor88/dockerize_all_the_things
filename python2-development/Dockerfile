FROM centos:7

MAINTAINER Tiago Paranhos Lima (tiago@tiagoprnl.me)

RUN yum update -y && yum install -y epel-release ; yum clean all 

RUN yum install -y ncdu wrk wrk2 siege curl wget \
                   vim tmux links elinks tree ; \
    yum clean all

RUN yum groupinstall -y "Development Tools" && \
    yum install -y zlib-devel bzip2-devel openssl-devel ncurses-devel \
                   sqlite-devel readline-devel tk-devel \
                   libxml2-devel libxslt-devel ;\
    yum clean all

# For ipython (notebook)
RUN yum install -y ncurses ncurses-devel ncurses-libs \
                   ncurses-base ncurses-term ;\
    yum clean all

# Requirements for matplotlib
RUN yum install -y libpng libpng-devel freetype freetype-devel ;\
    yum clean all

RUN yum install -y python-devel python-virtualenv sqlite sqlite-devel; \
    yum clean all

RUN yum install -y libffi libffi-devel openssl openssl-libs openssl-devel ; \
    yum clean all

RUN mkdir /build
WORKDIR /build

# Manually upgrade python to 2.7.10
RUN wget https://www.python.org/ftp/python/2.7.10/Python-2.7.10.tgz && tar xzf Python-2.7.10.tgz && cd Python-2.7.10 && ./configure && make install && cd .. && python --version

# Install pip manually, from yum I was getting an error trying to 
# upgrade it.
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
RUN python get-pip.py 

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

# Install IPython 
RUN pip install -U "ipython[all]"

# NLTK
RUN printf 'Installing NLTK...[WAIT]'
RUN pip install -U textblob nltk
RUN printf 'Installing NLTK...[DONE]'

# necessary for textblob to work as desired
RUN python -m textblob.download_corpora

# Install the core tools 
RUN pip install -U  numpy
# RUN pip install -U  scipy
RUN pip install -U  matplotlib

RUN pip install -U "pandas>=0.14.0"
RUN pip install -U "scikit-learn>=0.14.0"

# Install your specific project requirements:
ADD requirements* /build/

# Install your specific python project requirements...
RUN printf 'python requirements...[WAIT]'
RUN pip install -r requirements.txt
RUN printf 'python requirements...[DONE]'

WORKDIR /code


