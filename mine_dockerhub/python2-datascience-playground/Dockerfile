# python-datascience-playground
FROM tiagoprn/python2-development-base:v0.1

MAINTAINER Tiago Paranhos Lima (tiago@tiagoprnl.me)

USER root

RUN yum update -y ; yum clean all 

WORKDIR /build

# NLTK
RUN printf 'Installing NLTK...[WAIT]'
RUN pip install -U textblob nltk
RUN printf 'Installing NLTK...[DONE]'

# necessary for textblob to work as desired
RUN python -m textblob.download_corpora

# numpy, scipy, matpotlib
RUN pip install -U  numpy
RUN pip install -U  matplotlib

# For performance improvements to pandas
# numexpr     - Fast numerical expression evaluator for NumPy
RUN pip install -U numexpr
# Bottleneck     - Fast NumPy array functions written in Cython
RUN pip install -U Bottleneck
RUN pip install -U pandas

# TODO: Add in the future (specially scikit-learn is problematic to install)
# RUN pip install -U  scipy
# RUN pip install -U scikit-learn

# Install your specific project requirements:
ADD requirements* /build/

# Install your specific python project requirements...
RUN printf 'python requirements...[WAIT]'
RUN pip install -r requirements.txt
RUN printf 'python requirements...[DONE]'

USER appuser

WORKDIR /code

