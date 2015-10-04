# python2-base

FROM centos:7

MAINTAINER Tiago Paranhos Lima (tiago@tiagoprnl.me)

RUN yum update -y && yum install -y epel-release ; yum clean all 

RUN yum install -y ncdu wrk wrk2 siege curl wget \
                   vim links elinks tree ; \
    yum clean all

RUN yum groupinstall -y "Development Tools" && \
    yum install -y zlib-devel bzip2-devel openssl-devel ncurses-devel \
                   sqlite-devel readline-devel tk-devel \
                   libxml2-devel libxslt-devel ;\
    yum clean all

RUN yum install -y ncurses ncurses-devel ncurses-libs \
                   ncurses-base ncurses-term ;\
    yum clean all

RUN yum install -y libpng libpng-devel freetype freetype-devel ;\
    yum clean all

RUN yum install -y python-devel python-virtualenv sqlite sqlite-devel; \
    yum clean all

RUN yum install -y libffi libffi-devel openssl openssl-libs openssl-devel ; \
    yum clean all

RUN yum install -y ctags fontconfig fontconfig-devel sudo libevent libevent-devel; \
    yum clean all

RUN mkdir /build
WORKDIR /build

# Manually upgrade python to 2.7.10
RUN wget https://www.python.org/ftp/python/2.7.10/Python-2.7.10.tgz && tar xzf Python-2.7.10.tgz && cd Python-2.7.10 && ./configure && make install && cd .. && python --version

# Install pip manually, from yum I was getting an error trying to 
# upgrade it.
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
RUN python get-pip.py 

RUN printf 'Compiling and installing tmux...[WAIT]'
RUN wget https://github.com/tmux/tmux/releases/download/2.0/tmux-2.0.tar.gz && tar xfzv tmux-2.0.tar.gz
RUN cd tmux-2.0 && ./configure && make && make install && cd ..
RUN printf 'Compiling and installing tmux...[DONE]'

RUN pip install flake8 
RUN pip install powerline-status

RUN cp /usr/local/lib/python2.7/site-packages/powerline/bindings/bash/powerline.sh /tmp && \
    chmod 777 /tmp/powerline.sh

# Install your specific project requirements:
ADD requirements* /build/

# Install your specific python project requirements...
RUN printf 'python requirements...[WAIT]'
RUN pip install -r requirements.txt
RUN printf 'python requirements...[DONE]'

# create a new user that the application would run as
RUN adduser --uid 1000  appuser 
USER appuser

WORKDIR /home/appuser

RUN mkdir -p ~/.fonts ~/.config/fontconfig/conf.d && \
    curl https://raw.githubusercontent.com/powerline/powerline/develop/font/PowerlineSymbols.otf -o ~/.fonts/PowerlineSymbols.otf && \
    curl https://raw.githubusercontent.com/powerline/powerline/develop/font/10-powerline-symbols.conf -o ~/.config/fontconfig/conf.d/10-powerline-symbols.conf && \
    fc-cache -r ~/.fonts

RUN git clone https://github.com/tiagoprn/dot_files

RUN ln -s /home/appuser/dot_files/flake8 /home/appuser/.config/flake8 && \
    ln -s /home/appuser/dot_files/.vimrc /home/appuser/.vimrc && \
    ln -s /home/appuser/dot_files/.vim /home/appuser/.vim && \
    mkdir /home/appuser/.vim/bundle && \
    git clone https://github.com/gmarik/vundle.git /home/appuser/.vim/bundle/vundle

RUN mkdir /home/appuser/.tmux && \
    ln -s /home/appuser/dot_files/.tmux.conf /home/appuser/.tmux.conf && \
    git clone https://github.com/tmux-plugins/tpm /home/appuser/.tmux/plugins/tpm

USER root

RUN echo 'appuser ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

USER appuser

WORKDIR /code

