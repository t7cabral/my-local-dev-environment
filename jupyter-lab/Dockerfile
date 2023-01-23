FROM ubuntu:23.04

LABEL description="Ambiente Jupyter-lab"

LABEL version="1.0.0"

# Instalando dependencias do sistema
RUN apt-get update -y \
  && apt-get install python3-pip -y

# Instalando as libs usadas no projeto
RUN mkdir /home/ubuntu/sd-local_environment_data

WORKDIR /home/ubuntu/sd-local_environment_data

COPY requirements.txt .

COPY constraints.txt .

RUN pip3 install -r requirements.txt -c constraints.txt

RUN rm requirements.txt constraints.txt

CMD ["jupyter-lab", "--allow-root", "--port=8888", "--no-browser", "--ip=0.0.0.0"]
