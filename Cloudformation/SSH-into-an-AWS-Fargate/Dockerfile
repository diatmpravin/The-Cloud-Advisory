FROM nginx:latest
COPY ./index.html /usr/share/nginx/html/index.html

RUN apt-get install -y openssh-server

RUN echo $SSH_PUBLIC_KEY > ~/.ssh/authorized_keys

