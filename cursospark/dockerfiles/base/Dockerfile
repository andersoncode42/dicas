#
# Imagem que servirá como base das outras imagens usadas para o curso
# Aqui deverá conter as aplicações e configurações em comun de Todas as imagens
#
# IMPORTANTE: Esta imagem NÃO tem qualquer segurança
#             NÂO use em produção

FROM alpine:latest


# Variáveis de ambiente que usaremos para configurar os próximos passos
ENV USUARIO spark
ENV SENHA spark
ENV PASTA_USUARIO /home/$USUARIO


# Instala os pacotes necessários em sua última versão
RUN    apk add --update --no-cache \
               bash       \
               curl       \
               sudo       \
               vim        \
               nano       \
               openjdk11  \
    # Cria o usuário sem senha com sua respectivapasta home
    && adduser -D -h ${PASTA_USUARIO} ${USUARIO} \
    # # Preenche a senha do usuário
    && echo "${USUARIO}:${SENHA}" | chpasswd     \
    # Adicione o usuário ao grupo de superusuários(sudoers)
    && echo "${USUARIO} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
    # Para alterar o terminal para exibir o nome do usuário e a pasta
    && echo "PS1=\"\\u:\\W$ \"" >> ~/.bashrc

# Configura o diretório de trabalho no container
WORKDIR ${PASTA_USUARIO}

# Dizer ao container que todos os futuros comandos devem ser executados como esse usuário
USER ${USUARIO}

# Copiar algum arquivo para a pasta inicial do usuário spark (opcional)
# COPY --chown=${USUARIO} some-file.txt .

# Comando a executar quando iniciar o container
CMD ["bash"]

#-------------------------------------------
# Exemplo de como usar este dockerfile
#--------------------------------------------
# Entre na mesma pasta do arquivo "Dockerfile" e execute os comandos abaixo:
#
# Constrói localmente a imagem na sua máquina com a tag "cursospark-base"
# docker build -t "andersoncode42/cursospark:base" .
#
# Cria e roda um container baseado nesta imagem
# docker run --name cursospark-base -it "andersoncode42/cursospark:base"
#

