FROM python:3.12-alpine3.19
WORKDIR /app
COPY requirements.txt .
RUN apk update && apk upgrade --no-cache && pip install --upgrade pip && pip install -r requirements.txt
COPY app.py .
CMD ["python", "app.py"]
