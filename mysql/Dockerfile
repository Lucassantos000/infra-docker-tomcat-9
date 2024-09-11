FROM mysql:8.0-debian

# Atualizar os repositórios e instalar pacotes
USER root
RUN apt-get update && apt-get install -y \
    nano \
    curl \
    wget \
    iputils-ping \
    dnsutils \
    iproute2 \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Expor a porta do MySQL
EXPOSE 3306
