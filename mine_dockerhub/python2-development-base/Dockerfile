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

# Install ipython for jupyter notebooks support 
RUN pip install -U "ipython[all]"
RUN pip install ipywidgets

RUN pip install flake8 

# Install your specific project requirements:
ADD requirements* /build/

# Install your specific python project requirements...
RUN printf 'python requirements...[WAIT]'
RUN pip install -r requirements.txt
RUN printf 'python requirements...[DONE]'

RUN yum install ctags

# create a new user that the application would run as
RUN adduser --uid 1000  appuser 
USER appuser

WORKDIR /home/appuser

RUN git clone https://github.com/tiagoprn/dot_files

RUN mkdir /home/appuser/.config && \
          ln -s /home/appuser/dot_files/flake8 /home/appuser/.config/flake8 && \
          ln -s /home/appuser/dot_files/.vimrc /home/appuser/.vimrc && \
          ln -s /home/appuser/dot_files/.vim /home/appuser/.vim && \
          mkdir /home/appuser/.vim/bundle && \
          git clone https://github.com/gmarik/vundle.git /home/appuser/.vim/bundle/vundle

RUN mkdir /home/appuser/.tmux && \
    ln -s /home/appuser/dot_files/.tmux.conf /home/appuser/.tmux.conf && \
    git clone https://github.com/tmux-plugins/tpm /home/appuser/.tmux/plugins/tpm
WORKDIR /code

