FROM ubuntu

RUN apt-get install -y python
RUN apt-get update && apt-get install -y procps
# RUN apt-get install -y build-essential
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup | bash -
RUN apt-get install -y nodejs

RUN apt-get install -y git
RUN git clone https://github.com/mozilla/openbadges-badgekit.git
RUN apt-get install -y make
RUN apt-get install -y g++
RUN cd openbadges-badgekit && npm install
ADD config.json /openbadges-badgekit/config.json

CMD cd openbadges-badgekit && npm start 


