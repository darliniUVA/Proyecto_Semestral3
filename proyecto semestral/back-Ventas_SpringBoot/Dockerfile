# --- ETAPA 1: Compilación (Build con Maven estándar) ---
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /app

# Entramos y copiamos desde la subcarpeta correcta de Ventas
COPY Springboot-API-REST/pom.xml .
RUN mvn dependency:go-offline -B

COPY Springboot-API-REST/src ./src
RUN mvn clean package -DskipTests

# --- ETAPA 2: Ejecución (Imagen Liviana de Producción) ---
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Requisito Pauta: Crear un usuario no-root por seguridad
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

# Copiamos el archivo .jar generado
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]