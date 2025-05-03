創建 Dockerfile

echo. > Dockerfile

將下列內容貼進 Dockerfile 中：

# 使用官方 Python 映像檔
FROM python:3.12.10

# 設定工作目錄
WORKDIR /app

# 安裝 Poetry
RUN pip install poetry

# 複製專案核心設定檔
COPY pyproject.toml poetry.lock README.md ./

# 安裝依賴，不創建虛擬環境
RUN poetry config virtualenvs.create false && poetry install --no-root --no-interaction --no-ansi

# 複製剩下所有檔案
COPY . .

# 複製啟動腳本
COPY start.sh /app/start.sh

# 確保腳本可執行
RUN chmod +x /app/start.sh

# 容器啟動執行腳本
CMD ["bash", "/app/start.sh"]

________________________________________________________________________________________________________________________________________

創建 .dockerignore

echo. > .dockerignore

創建 README.md

echo "# my_workspace" > README.md

Step 2：建置 Docker 映像檔

docker build -t my-image-name .

Step 3：執行容器

docker run --rm my-image-name

如需進入容器內部（互動模式）：

docker run -it my-image-name /bin/bash

Step 4：安裝 ChromeDriver 所需套件（容器內執行）

apt-get update

apt-get install -y \
    libnss3 \
    libgconf-2-4 \
    libxi6 \
    libgdk-pixbuf2.0-0 \
    libasound2 \
    curl \
    unzip \
    libglib2.0-0 \
    libxcb1
    
Step 5：下載並安裝 ChromeDriver

CHROME_DRIVER_VERSION=$(curl -sS https://chromedriver.storage.googleapis.com/LATEST_RELEASE)

curl -O https://chromedriver.storage.googleapis.com/${CHROME_DRIVER_VERSION}/chromedriver_linux64.zip

unzip chromedriver_linux64.zip

mv chromedriver /usr/bin/

chmod +x /usr/bin/chromedriver

確認是否安裝成功：

/usr/bin/chromedriver --version

Step 6：在 Poetry 中安裝 webdriver_manager

poetry add webdriver_manager

Step 7：範例 Python 程式碼（使用 webdriver_manager）

from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
from webdriver_manager.chrome import ChromeDriverManager

options = Options()
options.add_argument("--headless")  # 如果你要無頭模式
service = Service(ChromeDriverManager().install())

driver = webdriver.Chrome(service=service, options=options)
driver.get("https://www.google.com")
print(driver.title)
driver.quit()
