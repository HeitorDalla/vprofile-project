# IMAGEM BASE - essa imagem vai gerar o artefato (.war, .jar)
FROM maven:3.9.9-eclipse-temurin-21-jammy as BUILD_IMAGE

# VAI EXECUTAR OS COMANDOS
RUN git clone https://github.com/HeitorDalla/vprofile-project.git
RUN cd vprofile-project && git checkout containers && mvn clean install

# IMAGEM BASE - essa imagem vai pegar o artefato gerado e rodar junto ao tomcat
FROM tomcat:10-jdk21

# LABELS 
LABEL "Project"="Vprofile"
LABEL "Author"="Heitor"

# APLICAÇÃO PADRÃO QUE PRECISA SER REMOVIDA
RUN rm -rf /usr/local/tomcat/webapps/*

# COPIAR O ARTEFATO DA IMAGEM 'BUILD_IMAGE' PARA ESSE IMAGEM  // COPY <origem> <destino>
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# PORTA EXPECIFICA QUE SERA RODADO A APLICACAO (TOMCAT VAI RODAR DENTRO DESSA PORTA NO CONTAINER)
EXPOSE 8080

# COMANDO QUE RODARÁ O SERVIDOR DO TOMCAT (O ARQUIVO 'catalina.sh' É O SCRIPT/COMANDO QUE INICIA O TOMCAT POR PADRÃO)
CMD ["catalina.sh", "run"]