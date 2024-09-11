FROM tomcat:9.0.79

# Atualizar os repositórios e instalar pacotes
RUN apt-get update && apt-get install -y \
    nano \
    curl \
    wget \
    iputils-ping \
    dnsutils \
    iproute2 \
    mysql-client || apt-get --fix-missing install

# Limpar cache para reduzir o tamanho da imagem
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Copiar o arquivo WAR
# COPY target/*.war /usr/local/tomcat/webapps/ROOT.war

# Expor porta 8080
EXPOSE 8080

# Iniciar o Tomcat
CMD ["catalina.sh", "run"]
