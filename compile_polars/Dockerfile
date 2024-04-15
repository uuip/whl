FROM python:3.12 as builder
RUN sed -i 's|http://deb.debian.org|http://mirrors.ustc.edu.cn|g' /etc/apt/sources.list.d/debian.sources \
    && apt-get update&&apt install -y build-essential cmake&&curl --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y&&pip3 install maturin
ARG polars_version
ADD polars-${polars_version}.tar.gz .
WORKDIR polars-${polars_version}
ENV JEMALLOC_SYS_WITH_LG_PAGE=16
ENV PATH /root/.cargo/bin:$PATH
RUN maturin build --release

FROM scratch AS export

ARG polars_version
COPY --from=builder /polars-${polars_version}/target/wheels/*.whl .

