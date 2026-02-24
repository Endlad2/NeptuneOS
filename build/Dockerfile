FROM ubuntu:latest

# Аргументы сборки с значениями по умолчанию
ARG ARCH=amd64
ARG BUILD_TYPE=release

# Предотвращаем интерактивные запросы при установке пакетов
ENV DEBIAN_FRONTEND=noninteractive

# Устанавливаем необходимые пакеты
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-venv \
    libxml2-utils \
    git \
    && rm -rf /var/lib/apt/lists/*

# Настройка Python
RUN ln -s /usr/bin/python3 /usr/bin/python

# Устанавливаем Python-пакеты
RUN pip3 install --no-cache-dir \
    jinja2 \
    future \
    ply \
    setuptools \
    six \
    lxml

WORKDIR /workspace

# Клонируем репозиторий
RUN git clone https://github.com/cl91/NeptuneOS.git

WORKDIR /workspace/NeptuneOS

# Инициализируем сабмодули
RUN git submodule update --init --recursive

# Делаем build.sh исполняемым
RUN chmod +x build.sh

# Запускаем сборку с переданными аргументами
RUN echo "Запуск сборки с ARCH=${ARCH}, BUILD_TYPE=${BUILD_TYPE}" && \
    ./build.sh ${ARCH} ${BUILD_TYPE}

CMD ["/bin/bash"]
