FROM python:3.6
ENV PYTHONUNBUFFERED=1
ENV PYTHONIOENCODING=UTF-8
COPY . /app/
WORKDIR /app/
RUN pip3 install -r /app/requirements.txt
RUN pip install kombu==4.4.0
EXPOSE 80
CMD ["python", "manage.py", "runserver", "0.0.0.0:80"]
