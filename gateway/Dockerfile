FROM maven:3-openjdk-17-slim as builder

# Define o diretório de trabalho
WORKDIR /builder

# Copia o código-fonte do projeto para o container
COPY . .

# Compila e empacota o projeto, ignorando os testes
RUN mvn clean package -DskipTests --batch-mode

FROM openjdk:17-jdk-alpine

# Copia o JAR gerado na etapa de build para esta imagem
COPY --from=builder /builder/target/*.jar /app.jar

# Expose the application port
EXPOSE 8082

# Run the App
ENTRYPOINT ["java", "-jar", "app.jar"]