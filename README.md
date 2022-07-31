# python_docker_tutorial_fastapi

- 練習程式碼 youtube
<https://youtu.be/bi0cKgmRuiA>

- 爬蟲程式碼參考
<https://github.com/python-engineer/python-fun/blob/master/moviepicker/main.py>

- FastAPI
<https://fastapi.tiangolo.com>

## docker 經常使用指令

```bash
# 查詢 docker 版本
$ docker -v

# 查詢 docker container info
$ docker ps -a

# 查詢 docker images info
$ docker images

# 建立 image
$ docker build -t XXX

# 執行 image
$ docker run XXX

```

## python-requests-app command

```bash

# 進入到對應資料夾內執行下方操作
$ cd python-requests-app

# 建構 python-imdb image 將 Dockerfile 相關檔案以及執行方式放置到 python-imdb image
$ docker build -t python-imdb .

# 執行docker run 不需要再對應資料夾內，可在根目錄執行，因為已經建立好 image

# 執行 python-imdb image，但每次執行都會新增一個 Container
# 假設 主要程式碼內有互動式問答輸入 docker run python-imdb 會下方錯誤
$ docker run python-imdb                                                      ok | 17s | 20:14:14 
神隱少女 (2001), Rating: 8.5, Starring: Hayao Miyazaki (dir.), Daveigh Chase, Suzanne Pleshette
Do you want another movie (y/[n])? Traceback (most recent call last):
  File "./main.py", line 44, in <module>
    main()
  File "./main.py", line 38, in main
    user_input = input('Do you want another movie (y/[n])? ')
EOFError: EOF when reading a line

# 如果有互動式問答則要輸入下方指令才可正常操作
$ docker run -t -i python-imdb                                                   1 err | 20:17:43 
天外奇蹟 (2009), Rating: 8.2, Starring: Pete Docter (dir.), Edward Asner, Jordan Nagai
Do you want another movie (y/[n])? y
阿拉伯的勞倫斯 (1962), Rating: 8.3, Starring: David Lean (dir.), Peter O'Toole, Alec Guinness
Do you want another movie (y/[n])? y
可可夜總會 (2017), Rating: 8.3, Starring: Lee Unkrich (dir.), Anthony Gonzalez, Gael García Bernal
Do you want another movie (y/[n])? y
殺無赦 (1992), Rating: 8.2, Starring: Clint Eastwood (dir.), Clint Eastwood, Gene Hackman
Do you want another movie (y/[n])? n

```

### python-requests-app/dockerfile

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

## python-fastapi-app command

```bash

# 進入到對應資料夾內執行下方操作
$ cd python-fastapi-app

# 建構 python-fastapi-app image 將 Dockerfile 相關檔案以及執行方式放置到 python-fastapi-app image
$ docker build -t python-fastapi-app .

# 執行 python-fastapi-app image
# 可以正常啟動 Server，但點擊 http://0.0.0.0:8000 會顯示無法連上這個網站
# 因為沒有給予對應的port，因此會出現問題
$ docker run python-fastapi-app                         1 err | 10s | 23:38:14 
INFO:     Started server process [1]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)


# 需要加上參數 -p 8000:8000 對應到程式碼內的 port 才可以正常連接到 docker server
$ docker run -p 8000:8000 python-fastapi-app             ok | 2m 7s | 23:40:29 
INFO:     Started server process [1]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
INFO:     172.17.0.1:61568 - "GET / HTTP/1.1" 200 OK

# 輸入下方網址，可以獲取建立的 API 相關資訊，也可以進行測試
<http://0.0.0.0:8000/docs>

```

### python-fastapi-app/dockerfile

```bash
# python版本
FROM python:3.8

# 複製 requirements.txt到根目錄
COPY requirements.txt .

# 新增main.py到根目錄
ADD main.py .

# 執行 安裝 requirements.txt 套件
RUN pip install -r requirements.txt

# docker run 對應的image 會執行下方指令
CMD [ "python", "./main.py" ]
```
