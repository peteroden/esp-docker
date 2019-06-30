FROM python:alpine

RUN apk add --no-cache ca-certificates
RUN apk update && \
    apk upgrade && \
    rm -rf /var/lib/apt/lists/*

RUN apk add git wget ncurses-dev flex bison gperf cmake ninja ccache

ENV IDF_VERSION release/v3.3
ENV TOOLCHAIN_FILENAME xtensa-esp32-elf-gcc8_2_0-esp32-2019r1-linux-amd64

RUN cd /srv && \
    git clone --single-branch --depth=1 -b $IDF_VERSION --recursive https://github.com/espressif/esp-idf.git && \
    rm -rf /srv/esp-idf/.git
RUN wget -nv https://dl.espressif.com/dl/${TOOLCHAIN_FILENAME}.tar.gz && \
    tar -xzf ${TOOLCHAIN_FILENAME}.tar.gz && \
    rm -f ${TOOLCHAIN_FILENAME}.tar.gz

ENV PATH=/srv/xtensa-esp32-elf/bin:/srv/esp-idf/tools:$PATH
ENV IDF_PATH=/srv/esp-idf
