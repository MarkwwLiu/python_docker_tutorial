# python_docker_tutorial_fastapi

- 爬蟲程式碼參考
https://github.com/python-engineer/python-fun/blob/master/moviepicker/main.py

- 練習youtube
https://youtu.be/bi0cKgmRuiA

- 使用指令

```bash
# 查詢 docker 版本
$ docker -v

# 建構 python-imdb image 將 Dockerfile 相關檔案以及執行方式放置到 python-imdb image
$ docker build -t python-imdb .

# 執行 python-imdb image，但每次執行都會新增一個
$ docker run python-imdb
```

## dockerfile 簡介

```bash
# python版本
FROM python:3.8

# 新增main.py到根目錄
ADD main.py .

# 執行 安裝 requests, beautifulsoup4
RUN pip install requests beautifulsoup4

# docker run 對應的image 會執行下方指令
CMD [ "python", "./main.py" ]
```
