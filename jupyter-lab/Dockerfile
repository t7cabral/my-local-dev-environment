FROM ubuntu:23.04
LABEL description="Ambiente Jupyter-lab"
LABEL version="1.0.0"

# Instalando dependencias do S.O
RUN \
  apt-get -y update && \
  apt-get install -y openjdk-8-jdk && \
  apt-get -y install python3-pip

# Pasta do projeto
RUN mkdir /home/ubuntu/sd-local_environment_data
WORKDIR /home/ubuntu/sd-local_environment_data

# Instalando as libs do Python
COPY requirements.txt .
COPY constraints.txt .
RUN pip3 install -r requirements.txt -c constraints.txt --break-system-packages
RUN rm requirements.txt constraints.txt

CMD ["jupyter-lab", "--allow-root", "--port=8888", "--no-browser", "--ip=0.0.0.0"]
