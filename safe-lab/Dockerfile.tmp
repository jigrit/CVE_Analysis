FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

# sudo 소스 빌드에 필요한 도구 및 의존성 설치
RUN apt-get update && \
    apt-get install -y build-essential wget libpam0g-dev \
                       libselinux1-dev zlib1g-dev vim \
                       pkg-config libssl-dev git ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# sudo 1.9.17 소스 다운로드 및 설치
WORKDIR /usr/src
RUN wget https://www.sudo.ws/dist/sudo-1.9.17.tar.gz && \
    tar xzf sudo-1.9.17.tar.gz && \
    cd sudo-1.9.17 && \
    ./configure --disable-gcrypt --prefix=/usr && \
    make && \
    make install

# 일반 권한 사용자 생성
RUN useradd -m -s /bin/bash lowpriv

# 컨테이너 실행 시 일반 권한 사용자로 시작
USER lowpriv
WORKDIR /home/lowpriv

CMD ["/bin/bash"]


