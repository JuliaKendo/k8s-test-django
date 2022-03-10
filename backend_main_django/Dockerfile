FROM nginx/unit:1.25.0-python3.9
ENV PYTHONUNBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1

ENV SECRET_KEY=12345
ENV DEBUG=FALSE
ENV ALLOWED_HOSTS=*
ENV DATABASE_URL=postgres://postgres:12345@85.175.101.149:6767/test

RUN mkdir /code
WORKDIR /code
COPY requirements.txt /code/
RUN apt update && apt install -y python3-pip                                  \
    && pip3 install -r requirements.txt                                       \
    && apt remove -y python3-pip                                              \
    && apt autoremove --purge -y                                              \
    && rm -rf /var/lib/apt/lists/* /etc/apt/sources.list.d/*.list
COPY unit_config.json /docker-entrypoint.d/
COPY . /code/
RUN SECRET_KEY=${SECRET_KEY} python manage.py collectstatic --noinput
EXPOSE 80
VOLUME ["/media"]
