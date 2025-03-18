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
                        python3 \
                        python3-pip \
                        python3-venv \
    && rm -rf /var/lib/apt/lists/*

# Create and activate virtual environment, then install dependencies
RUN python3 -m venv /opt/venv
RUN /opt/venv/bin/pip install flask

# Copy the server script
COPY server.py /root/server.py
COPY source.py /root/source.py
COPY public.txt /root/public.txt
COPY private.txt /root/private.txt

# Start SSH and the server
CMD /opt/venv/bin/python /root/server.py