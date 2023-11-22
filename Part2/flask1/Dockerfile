FROM python:3.9.18-bookworm
WORKDIR /app
COPY . /app/
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python", "app.py"]