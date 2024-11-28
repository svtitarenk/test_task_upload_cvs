FROM python:3.9-slim

# Установка системных зависимостей
RUN apt-get update && apt-get install -y \
    build-essential \
    libssl-dev \
    libpq-dev \
    libffi-dev \
    python3-dev \
    curl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app/api

# Копируем зависимости
COPY ./requirements.txt /app/api/requirements.txt

# Установка Python-зависимостей
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

# Копируем файлы приложения
COPY ./ /app/api
COPY ./ /app/lib

# Настройка PYTHONPATH
ENV PYTHONPATH="/app/lib:${PYTHONPATH}"

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
