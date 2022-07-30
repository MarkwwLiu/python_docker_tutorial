# python_docker_tutorial_fastapi

- 爬蟲程式碼參考
<https://github.com/python-engineer/python-fun/blob/master/moviepicker/main.py>

- 練習youtube
<https://youtu.be/bi0cKgmRuiA>

- 使用指令

```bash
# 查詢 docker 版本
$ docker -v

# 建構 python-imdb image 將 Dockerfile 相關檔案以及執行方式放置到 python-imdb image
$ docker build -t python-imdb .

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
