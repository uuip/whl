FROM python:3.11
RUN sed -i 's|http://deb.debian.org|http://mirrors.ustc.edu.cn|g' /etc/apt/sources.list.d/debian.sources \
    && apt-get update&&apt install -y build-essential cmake&&curl --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y&&pip3 install maturin
ADD polars-0.20.3.tar.gz .
WORKDIR polars-0.20.3
ENV JEMALLOC_SYS_WITH_LG_PAGE=16
ENV PATH /root/.cargo/bin:$PATH
RUN maturin build --release

