FROM ruby:3.3.0
RUN apt-get update -qq && apt-get install -y vim 

RUN apt-get install libmecab2 libmecab-dev mecab unidic-mecab mecab-utils 
RUN apt-get install -y build-essential

RUN mkdir /usr/src/app 
WORKDIR /usr/src/app
COPY Gemfile /usr/src/app/Gemfile 
COPY Gemfile.lock /usr/src/app/Gemfile.lock 
COPY mecabrc /etc/mecabrc

RUN gem update --system 
RUN bundle update --bundler 

RUN bundle install 
COPY . /usr/src/app 

COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh 
ENTRYPOINT ["entrypoint.sh"]