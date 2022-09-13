# syntax=docker/dockerfile:1

FROM python:3.6

WORKDIR /app

COPY . .

RUN pip3 install -r requirements.txt


# build app for production with minification
EXPOSE 8085
CMD [ "python3", "-u", "main.py" ]
