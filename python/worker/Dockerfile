FROM python:3.6
COPY . /app/
WORKDIR /app/
RUN pip3 install -r /app/requirements.txt
RUN pip install kombu==4.4.0
EXPOSE 80
CMD ["celery", "worker", "-A", "app", "--loglevel=INFO"]
