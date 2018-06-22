FROM python:3.4

RUN apt-get update && apt-get install -y \
  libblas-dev liblapack-dev libatlas-base-dev \
  gfortran && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

# Pandas >=0.21 is incompatible with Python 3.4
# see https://github.com/pandas-dev/pandas/issues/20723
RUN pip --no-cache-dir install \
  ipykernel scipy jupyter matplotlib 'pandas<0.21' elasticsearch && \
  python -m ipykernel.kernelspec

COPY ./config/jupyter_notebook_config.py /root/.jupyter/

# Jupyter has issues with being run directly:
# https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY ./config/run_jupyter.sh /

# Jupyter
EXPOSE 8888

VOLUME "/notebooks"
WORKDIR "/notebooks"

CMD ["/run_jupyter.sh"]
