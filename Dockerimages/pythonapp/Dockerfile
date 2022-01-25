FROM  oraclelinux:8.4 
# base docker image for python code integration  / running 
# if not present in Docker engine then will be pulled from docker hub
LABEL name="ashutoshh"
LABEL email="ashutoshh@linux.com"
# just image designer info details 
# label is an optional field 
RUN dnf install python3 -y 
# to get the shell during image build time 
# YUM is a software installer in oracle Linux 
RUN mkdir  /myapp 
COPY test.py /myapp/test.py
# copy data from docker client machine to docker engine during  image build time
# newly created docker image will contain that code 
CMD ["python3","/myapp/test.py"]
# use of CMD is to define default parent process
# for image 
