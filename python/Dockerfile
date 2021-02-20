# FROM python:3.6
# ENV PYTHONUNBUFFERED=1
# ENV PYTHONIOENCODING=UTF-8
# COPY . /app/
# WORKDIR /app/
# RUN pip3 install -r /app/requirements.txt
# RUN pip install kombu==4.4.0
# EXPOSE 80
# # using here manage.py server instead of guincorn server because this dockerfile for development env
# CMD ["python", "manage.py", "runserver", "0.0.0.0:80"]

# -------------------- another incridible one ----------------------
FROM python:3.6
RUN apt-get update -y  && apt-get install supervisor nginx  -y
RUN mkdir -p /home/ubuntu/main/
RUN mkdir -p /home/ubuntu/main/run
RUN curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.2.0-amd64.deb
RUN dpkg -i filebeat-7.2.0-amd64.deb
COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY filebeat.yml /etc/filebeat/filebeat.yml
COPY nginx.yml   /etc/filebeat/modules.d/nginx.yml
RUN  filebeat modules enable nginx
COPY ./default.conf /etc/nginx/sites-available/default
RUN mkdir /home/ubuntu/main/bin
COPY ./bin/ /home/ubuntu/main/bin
RUN pip install daphne
# instead of only run "RUN easy_install gunicorn" command will run the 3 programs [app(gunicorn),filebat and nginx] by supervisord
CMD ["/usr/bin/supervisord"]
