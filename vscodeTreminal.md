# 創建Dockerfile

如果你用的是 CMD，請打：

echo. > Dockerfile

-----------------------------------------------------------------------------------------------------------

# 複製貼上Dockerfile

# 使用官方 Python 映像檔
FROM python:3.12-slim

# 設定工作目錄
WORKDIR /app

# 安裝 poetry
RUN pip install poetry

# 複製必要檔案
COPY pyproject.toml poetry.lock README.md ./

# 安裝依賴（不建虛擬環境、也不裝目前專案）
RUN poetry config virtualenvs.create false && poetry install --no-root --no-interaction --no-ansi

# 複製剩下的所有檔案
COPY . .

# 預設執行指令
CMD ["python", "coffee/coffee.py"]

------------------------------------------------------------------------------------------------------------

# 創建 Dockerignore

echo. > .dockerignore

# 補一個 README.md

echo "# my_workspace" > README.md

# 建立 Docker 映像

docker build -t coffee .

# 執行容器

docker run --rm coffee

poetry.lock 檔案不匹配，Poetry 提示你需要重新生成 poetry.lock 檔案。

解決方案：

在本地執行 poetry lock 來更新 poetry.lock 檔案：

poetry lock

執行完後，會更新 poetry.lock 檔案，你可以再將它複製到 Docker 容器中。然後重新執行 Docker build：

docker build -t coffee .

# 進入容器

docker run -it coffee /bin/bash

# 下載Chromedriver相關的庫

apt-get update
apt-get install -y \
    libnss3 \
    libgconf-2-4 \
    libxi6 \
    libgdk-pixbuf2.0-0 \
    libasound2
    
# 安裝 curl

apt-get update
apt-get install -y curl
apt-get install -y unzip
apt-get install -y libglib2.0-0
apt-get install -y libnss3
apt-get install -y libxcb1

# 下載 chromedriver

CHROME_DRIVER_VERSION=$(curl -sS https://chromedriver.storage.googleapis.com/LATEST_RELEASE)
curl -O https://chromedriver.storage.googleapis.com/${CHROME_DRIVER_VERSION}/chromedriver_linux64.zip

# 解壓縮並移動 chromedriver

unzip chromedriver_linux64.zip
mv chromedriver /usr/bin/
chmod +x /usr/bin/chromedriver

# 確認安裝

/usr/bin/chromedriver --version

# 然後在你的 Poetry 環境中安裝 webdriver_manager

poetry add webdriver_manager

# 從新整理程式碼

from selenium import webdriver

from selenium.webdriver.chrome.service import Service

from selenium.webdriver.chrome.options import Options

from webdriver_manager.chrome import ChromeDriverManager



