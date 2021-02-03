FROM forsrc/raspbian:python

RUN apt-get -q update

RUN apt-get install -y libhdf5-dev libc-ares-dev libeigen3-dev gcc gfortran python-dev libgfortran5 \
                       libatlas3-base libatlas-base-dev libopenblas-dev libopenblas-base libblas-dev \
                       liblapack-dev cython libatlas-base-dev openmpi-bin libopenmpi-dev python3-dev \
                       wget curl ca-certificates

RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN wget https://bootstrap.pypa.io/get-pip.py
#RUN python get-pip.py
RUN python3 get-pip.py

RUN python3 -m pip install --upgrade pip
RUN pip3 install keras_applications==1.0.8 --no-deps
RUN pip3 install keras_preprocessing==1.1.0 --no-deps
RUN pip3 install h5py==2.10.0
RUN pip3 install pybind11
RUN pip3 install --upgrade setuptools
RUN pip3 install -U --user six wheel mock

WORKDIR /home/pi
RUN cd /home/pi



#ADD tensorflow-2.4.0-cp37-none-linux_armv7l.whl .

RUN curl -k -sc /tmp/cookie "https://drive.google.com/uc?export=download&id=11PQxiGqGszPKtWAWq8PXakyYyJU2ZARe" > /dev/null && \
    CODE="$(awk '/_warning_/ {print $NF}' /tmp/cookie)" && \
    curl -Lb /tmp/cookie "https://drive.google.com/uc?export=download&confirm=${CODE}&id=11PQxiGqGszPKtWAWq8PXakyYyJU2ZARe" -o tensorflow-2.4.0-cp37-none-linux_armv7l.whl

RUN pip3 uninstall tensorflow
RUN pip3 install tensorflow-2.4.0-cp37-none-linux_armv7l.whl
