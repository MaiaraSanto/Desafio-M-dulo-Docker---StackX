# Passo 1: Use a imagem oficial do nginx com a versão Alpine (leve)
FROM nginx:alpine

# Passo 2: Define o diretório de trabalho dentro do container
WORKDIR /app

# Passo 3: Copia o arquivo index.html para o diretório padrão do nginx
COPY index.html /usr/share/nginx/html/index.html

# Passo 4: Define uma variável de ambiente para a versão da aplicação
ENV APP_VERSION=1.0.0

# Passo 5: Instala os pacotes curl, htop e wget usando o gerenciador de pacotes do Alpine (apk)
RUN apk add --no-cache curl htop wget

# Passo 6: Expõe a porta 80 para acesso externo
EXPOSE 80

# Passo 7: Inicia o servidor nginx em primeiro plano
CMD ["nginx", "-g", "daemon off;"]

