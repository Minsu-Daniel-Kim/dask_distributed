FROM continuumio/miniconda3

# Dumb init
RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64
RUN apt-get update
RUN apt-get install build-essential -y
RUN chmod +x /usr/local/bin/dumb-init

RUN conda update conda && conda install "conda=4.4.7"
RUN conda install --yes \
    python-blosc \
    cytoolz \
    dask \
    distributed \
    nomkl \
    numpy \
    pandas \
    && conda clean -tipsy
    
RUN conda install -c anaconda pymysql -y

RUN conda install -c conda-forge opencv -y

RUN conda install -c bioconda/label/deprecated joblib -y

RUN conda install -c conda-forge pip -y

RUN pip install fancyimpute

COPY prepare.sh /usr/bin/prepare.sh
RUN chmod +x /usr/bin/prepare.sh

RUN mkdir /opt/app

ENTRYPOINT ["/usr/local/bin/dumb-init", "/usr/bin/prepare.sh"]
