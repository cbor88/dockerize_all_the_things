FROM python:2.7.10

MAINTAINER Tiago Paranhos Lima (tiago@tiagoprnl.me)

# Update and configure the distribution
RUN apt-get update -y && apt-get install -y locales && locale-gen en_US en_US.UTF-8

# mongodb-clients provides mongoexport
RUN apt-get install -y pypy mongodb-clients 

RUN pip install --upgrade pip

RUN pip install pkgconfig

RUN pip install cython

RUN pip install gevent

# Prepare the environment to build monary 
# (mongo-c-driver for performance on python):

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

# NLTK
RUN printf 'Installing NLTK...[WAIT]'
RUN pip install -U textblob nltk
RUN printf 'Installing NLTK...[DONE]'

# necessary for textblob to work as desired
RUN python -m textblob.download_corpora

# Install IPython 
RUN pip install -U "ipython[all]"

# Install the core tools 
RUN pip install -U  numpy scipy matplotlib
RUN pip install -U "pandas>=0.14.0"
RUN pip install -U "scikit-learn>=0.14.0"

# Install your specific project requirements:
RUN mkdir /build
ADD requirements* /build/
WORKDIR /build

# Install your specific python project requirements...
RUN printf 'python requirements...[WAIT]'
RUN pip install -r requirements.txt
RUN printf 'python requirements...[DONE]'

WORKDIR /code

# Cleaning up the image
RUN (apt-get autoremove -y; \
     apt-get clean -y)
