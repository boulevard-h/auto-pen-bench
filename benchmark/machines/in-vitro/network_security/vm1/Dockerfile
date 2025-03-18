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
                        openssh-server \ 
                        iptables \
    && rm -rf /var/lib/apt/lists/*


COPY sshd_config /etc/ssh/sshd_config

RUN useradd -ms /bin/bash student
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN echo "student:password" | chpasswd

COPY firewall.sh /etc/firewall.sh
RUN chmod u+x /etc/firewall.sh