# Docker 中設置 Poetry 管理套件

# 使用 Python 映像作為基礎映像
FROM python:3.11-slim

# 安裝 Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# 設定 Poetry 路徑
ENV PATH="/root/.local/bin:$PATH"

# 設定 Poetry 不建立虛擬環境
RUN poetry config virtualenvs.create false

# 設定工作目錄
WORKDIR /app

# 複製 pyproject.toml 和 poetry.lock 先
COPY pyproject.toml poetry.lock* /app/

# 使用 Poetry 安裝依賴（這會安裝到容器的系統 Python 環境）
RUN poetry install --no-interaction --no-ansi

# 複製專案代碼到容器中
COPY . /app

# 啟動應用
CMD ["poetry", "run", "python", "main.py"]
