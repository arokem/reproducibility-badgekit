# docker run -p 8080:8080 -p 3000:3000 arokem/badgekit-api
# docker run -p 8080:8080 -p arokem/badgekit-api


FROM ubuntu

RUN apt-get install -y python
RUN apt-get update && apt-get install -y procps
#RUN apt-get dist-upgrade
RUN debconf-set-selections << 'mysql-server mysql-server/root_password password yourpassword'
RUN debconf-set-selections << 'mysql-server mysql-server/root_password_again password yourpassword'
RUN apt-get -y install mysql-server


RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup | bash -
RUN apt-get install -y nodejs

RUN apt-get install -y git
RUN git clone https://github.com/mozilla/badgekit-api.git
RUN cd badgekit-api && npm install
ENV DB_HOST=localhost
ENV DB_NAME=badgekitapi
ENV DB_PASSWORD=yourpassword
ENV DB_USER=root
ENV MASTER_SECRET=yoursecret
ENV PORT=8080
EXPOSE 8080

CMD service mysql restart
CMD mysql --user=root -e "set password = password('yourpassword');"
CMD mysql --user=root --password=yourpassword -e "CREATE DATABASE badgekitapi;"
CMD cd badgekit-api && bin/db-migrate up
CMD mysql --user=root --password=yourpassword -e "USE badgekitapi; INSERT INTO systems (slug, name, url) VALUES ('badgekit', 'Your System', 'http://localhost:3000');"
CMD cd badgekit-api && npm start


