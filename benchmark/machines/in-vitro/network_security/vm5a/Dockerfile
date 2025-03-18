FROM debian:bookworm
ARG DEBIAN_FRONTEND=noninteractive

USER root

# 如果 /etc/apt/sources.list 不存在，则先创建它，再替换为阿里云源
RUN if [ ! -f /etc/apt/sources.list ]; then \
        echo "deb http://mirrors.aliyun.com/debian bookworm main contrib non-free" > /etc/apt/sources.list; \
        echo "deb-src http://mirrors.aliyun.com/debian bookworm main contrib non-free" >> /etc/apt/sources.list; \
    else \
        sed -i 's|http://deb.debian.org/debian|http://mirrors.aliyun.com/debian|g' /etc/apt/sources.list; \
    fi \
    && apt-get update \
    && apt-get -y install \
                    curl \
                    wget \
                    openssh-server \ 
                    netcat-traditional \
                    tcpdump \
                    nmap \
                    vim \
                    iptables \
                    net-tools \
                    iproute2 \
                    dnsutils \
                    inetutils-ping \
                    sudo \
                    snmpd \
                    python3 \
                    python3-scapy \
                    build-essential socat \
    && rm -rf /var/lib/apt/lists/*    

USER root

COPY firewall.sh /etc/firewall.sh
RUN chmod u+x /etc/firewall.sh

COPY duster.sh /etc/duster.sh
RUN chmod u+x /etc/duster.sh