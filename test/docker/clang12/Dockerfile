FROM debian:bullseye

ARG USE_SANITIZERS=OFF
ARG DEBIAN_FRONTEND=noninteractive

COPY /test/docker/install-clang.sh /
RUN /install-clang.sh 12

COPY . /pisa
RUN mkdir /pisa/build
WORKDIR /pisa/build

RUN cmake \
    -DCMAKE_BUILD_TYPE='Debug' \
    -DPISA_BUILD_TOOLS='OFF' \
    -DPISA_ENABLE_BENCHMARKING='OFF' \
    -DCMAKE_TOOLCHAIN_FILE='clang.cmake' \
    "-DPISA_SANITIZERS=$USE_SANITIZERS" \
    .. \
    && cmake --build . --config Debug -- -j 4

CMD ["ctest", "-VV", "-j", "4"]
