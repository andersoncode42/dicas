#
# Imagem que servirá como base das outras imagens usadas para o curso
# Aqui deverá conter as aplicações e configurações em comun de Todas as imagens
#
# IMPORTANTE: Esta imagem NÃO tem qualquer segurança
#             NÂO use em produção
# Use alpine as base image
FROM alpine:latest

# Instala os pacotes necessários
RUN    apk add --update --no-cache \
               bash       \
               curl       \
               sudo       \
               openssh    \
               vim        \
               nano       \
    # Create a user called spark with password spark and add it to sudoers
    && adduser -D spark              \
    && echo "spark:spark" | chpasswd \
    && echo "spark ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
    # Generate host keys for sshd
    && ssh-keygen -A \
    # Set PermitRootLogin to yes
    && sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Expose port 22 for ssh
EXPOSE 22

# Start sshd in the foreground
CMD ["/usr/sbin/sshd", "-D"]

#-------------------------------------------
# Exemplo de como usar este dockerfile
#--------------------------------------------
# Entre na mesma pasta do arquivo "Dockerfile" e execute os comandos abaixo:
#
# Constrói localmente a imagem na sua máquina com a tag "cursospark-base"
# docker build -t cursospark-base .
#
# Cria e roda um container baseado nesta imagem
# e amarra a porta 2222 do seu computador com a porta 22 do container
# docker run --name cursospark-base -d -p 2222:22 cursospark-base
#
# Acessa remotamente o container
# ssh-keygen -f "$HOME/.ssh/known_hosts" -R "[localhost]:2222"
# ssh spark@localhost -p 2222
