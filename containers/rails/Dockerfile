FROM ruby:2.3.1

RUN apt-get update
RUN apt-get install -y nodejs mysql-client --no-install-recommends sysv-rc-conf
RUN rm -rf /var/lib/apt/lists/*
RUN gem install rdoc-data; rdoc-data --install

EXPOSE 3000

ENTRYPOINT cd /usr/src/app; bundle install -j4; rake db:create; rake db:structure:load; rake db:migrate; rm /tmp/unicorn.pid; bundle exec unicorn -c config/unicorn.rb -E development; tail -f /dev/null

