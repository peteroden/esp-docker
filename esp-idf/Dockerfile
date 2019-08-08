FROM python:alpine

RUN apk add --no-cache ca-certificates
RUN apk update && \
    apk upgrade && \
    rm -rf /var/lib/apt/lists/*

RUN apk add git wget ncurses-dev flex bison gperf cmake ninja ccache

ENV IDF_VERSION v3.2.2
ENV TOOLCHAIN_FILENAME xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz

RUN mkdir /esp && \
    cd /esp && \
    git clone --single-branch --depth=1 -b $IDF_VERSION --recursive https://github.com/espressif/esp-idf.git && \
    rm -rf /srv/esp-idf/.git
RUN cd /esp/ && \
    wget -nv https://dl.espressif.com/dl/${TOOLCHAIN_FILENAME} && \
    tar -xzf ${TOOLCHAIN_FILENAME} && \
    rm -f ${TOOLCHAIN_FILENAME}

ENV PATH=/esp/xtensa-esp32-elf/bin:/esp/esp-idf/tools:$PATH
ENV IDF_PATH=/esp/esp-idf
