FROM ruby:3.3.0
RUN apt-get update -qq && apt-get install -y vim 

RUN apt-get install libmecab2 libmecab-dev mecab mecab-ipadic mecab-ipadic-utf8 mecab-utils
RUN apt-get install -y unidic-mecab unidic-mecab-utf8
RUN apt-get install -y build-essential

RUN mkdir /usr/src/app 
WORKDIR /usr/src/app
COPY Gemfile /usr/src/app/Gemfile 
COPY Gemfile.lock /usr/src/app/Gemfile.lock 
RUN sed -i 's/^dicdir/;dicdir/' /etc/mecabrc
RUN -e  "\ndicdir = /var/lib/mecab/dic/unidic" >> /etc/mecabrc

RUN gem update --system 
RUN bundle update --bundler 

RUN bundle install 
COPY . /usr/src/app 

COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh 
ENTRYPOINT ["entrypoint.sh"]