# Use uma imagem official do Python
FROM python:3

# Criar e usar um usuário não privilegiado
RUN groupadd -r appgroup && useradd -r -g appgroup appuser

# Definindo o diretório onde a aplicação será armazenada
WORKDIR /app

# Copiar os arquivos da pasta local para dentro do container
#COPY app.py Dockerfile ecs-task-definition.json requirements.txt sonar-project.properties test.py /app
COPY . /app

# Instalar as dependências de Python de acordo com o que foi desenvolvido na aplicação e que está declarado no arquivo requirements.txt.
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Alterar a propriedade dos arquivos copiados para o usuário não privilegiado
RUN chown -R appuser:appgroup /app

# Definir o usuário para rodar o container
USER appuser

# Garante que será iniciado a aplicação.
CMD ["gunicorn", "app:app"]