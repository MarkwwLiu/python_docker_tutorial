# Dockerfile, Image, Container
FROM python:3.8

COPY requirements.txt .

ADD main.py .

RUN pip install -r requirements.txt

CMD [ "python", "./main.py" ]