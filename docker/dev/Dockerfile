FROM ubuntu:bionic

RUN set -x && apt-get update -qq \
&& apt-get -y install \
  cmake make \
  llvm-7 clang-7 llvm-7-dev libclang-7-dev \
  odb libodb-sqlite-dev libodb-pgsql-dev \
  libsqlite3-dev \
  default-jdk \
  libssl1.0-dev \
  libgraphviz-dev \
  libmagic-dev \
  libgit2-dev \
  nodejs-dev node-gyp npm \
  ctags \
  wget \
  libgtest-dev \
  # Install boost libraries.
  libboost-filesystem-dev \
  libboost-log-dev \
  libboost-program-options-dev \
  libboost-regex-dev \
  # Build thrift.
  && wget "http://www.apache.org/dyn/mirrors/mirrors.cgi?action=download&filename=thrift/0.12.0/thrift-0.12.0.tar.gz" -O /opt/thrift-0.12.0.tar.gz; \
     tar -xf /opt/thrift-0.12.0.tar.gz -C /opt; \
     cd /opt/thrift-0.12.0; \
     ./configure --silent; \
     cd /; \
     make -C /opt/thrift-0.12.0 -j4 --silent install; \
     rm -rf /opt/thrift-0.12.0 /opt/thrift-0.12.0.tar.gz \
  # Build GTest.
  && cd /usr/src/googletest/ && \
     mkdir build && \
     cd build && \
     cmake .. && \
     make install && \
     cd / && \
     rm -rf /usr/src/googletest/build \
  \
  # Remove unnecessary packages.
  && apt-get purge -y --auto-remove wget \
  \
  # Erase downloaded archive files.
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/ \
  && set +x

COPY codecompass-build.sh /usr/local/bin

ENV DATABASE=sqlite BUILD_TYPE=Release
