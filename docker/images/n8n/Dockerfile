# Use a imagem base oficial do Python 3.9
FROM python:3.9-slim

# Defina o diretório de trabalho dentro do contêiner
WORKDIR /app

# Instale dependências necessárias
RUN apt-get update && apt-get install -y \
    curl \
    openssh-client \
    openssh-server \
    && rm -rf /var/lib/apt/lists/*

# Instale o FastAPI e o Uvicorn
RUN pip install fastapi uvicorn

# Crie um usuário não root para executar o aplicativo
RUN useradd -ms /bin/bash appuser
USER appuser

# Copie o código do aplicativo para o contêiner
COPY --chown=appuser:appuser . /app

# Exponha a porta que o FastAPI usará
EXPOSE 8000

# Comando para iniciar o servidor FastAPI usando o Uvicorn
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
