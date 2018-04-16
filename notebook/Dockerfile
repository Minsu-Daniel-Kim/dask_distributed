FROM jupyter/base-notebook

USER root
RUN apt-get update
RUN apt-get install -yq --no-install-recommends graphviz git vim
RUN apt-get install build-essential -y
RUN apt-get update 
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*
USER $NB_USER

RUN conda update conda && conda install "conda=4.4.7"
RUN conda config --add channels conda-forge
RUN conda config --add channels anaconda
RUN conda install --yes \
    python-blosc \
    cytoolz \
    dask==0.17.2  \
    distributed==1.21.6 \
    nomkl \
    numpy==1.14.2 \
    pandas==0.22.0 \
    ipywidgets \ 
    pymysql \ 
    opencv \ 
    pip \
    joblib \
    awscli \
    jupyterlab \
    && conda clean -tipsy

RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager@0.34.0
RUN jupyter labextension install qgrid

RUN pip install graphviz \
                --no-cache-dir \
                --no-dependencies

RUN pip install fancyimpute

USER root
COPY prepare.sh /usr/bin/prepare.sh
RUN chmod +x /usr/bin/prepare.sh
RUN mkdir /opt/app
COPY examples/ /home/$NB_USER/examples
RUN chown -R $NB_USER /home/$NB_USER/examples
USER $NB_USER

ENTRYPOINT ["tini", "--", "/usr/bin/prepare.sh"]
CMD ["start.sh jupyter lab"]
