# v20221028 by alex@rk86.com
FROM alex-redmine-base:503
# patches
WORKDIR /tmp
# COPY files/patch_20220518.diff .
# RUN patch /opt/bitnami/redmine/app/models/query.rb patch_20220518.diff
# end: patches
WORKDIR /opt/bitnami/redmine/public
COPY files/logo.png .
WORKDIR /opt/bitnami/redmine/plugins
# Let's install the plugins to allow the environment to build their dependencies
# Use specific release (when exists) instead clone since it may be not compatible with the current env
# RUN git clone https://github.com/anteo/redmine_custom_workflows.git
RUN wget https://github.com/anteo/redmine_custom_workflows/archive/refs/tags/v2.0.5.tar.gz -O - | tar -xz
RUN mv redmine_custom_workflows-2.0.5 redmine_custom_workflows
# RUN git clone https://github.com/jgraichen/redmine_dashboard.git
RUN wget https://github.com/jgraichen/redmine_dashboard/archive/refs/tags/v2.12.2.tar.gz -O - | tar -xz
RUN mv redmine_dashboard-2.12.2 redmine_dashboard
RUN git clone https://github.com/taqueci/redmine_local_avatars.git
# RUN git clone https://github.com/jkraemer/stopwatch.git
# RUN git clone https://github.com/Smile-SA/redmine_smile_togglesidebar.git - not compatible with redmine 5
# RUN git clone https://github.com/alphanodes/additionals.git
# RUN git clone https://github.com/tkusukawa/redmine_work_time.git
WORKDIR /opt/bitnami/redmine/
# USER bitnami
# rexml required for svn browse, not part of Ruby 3 as default
# RUN cat Gemfile
RUN echo >> Gemfile
RUN echo "gem 'rexml'" >> Gemfile
# bundle deployment
RUN bundle config unset deployment
RUN bundle install --no-deployment
# alexm:20210128, took me some time to figure out, https://github.com/danmunn/redmine_dmsf/issues/1094
# the line below is critical for redmine_custom_workflows, failing with multi threaded loading!
RUN sed -i -e 's/config.eager_load = true/config.eager_load = false/g' config/environments/production.rb
# Passenger in its Standalone mode, download necessary files (instead when docker starts)
RUN passenger-config install-standalone-runtime
RUN passenger-config build-native-support

# These lines to run after starting dockers and copying plugins manually: 
# docker cp YOUR_PLUGIN YOUR_REDMINE_CONTAINER:/opt/bitnami/redmine/plugins/
# docker exec -it YOUR_REDMINE_CONTAINER bundle exec rake redmine:plugins NAME=YOUR_PLUGIN RAILS_ENV=production
