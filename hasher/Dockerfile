# Fetch the image from Docer Hub
FROM ruby:alpine

# Run installations needed for running the application 
RUN apk add --update build-base curl 
RUN gem install sinatra
RUN gem install thin

# Run the Ruby file 
ADD hasher.rb /
CMD ["ruby", "hasher.rb"]

# Expose the needed port for the application and perform a healthcheck
EXPOSE 80
HEALTHCHECK \
  --interval=1s --timeout=2s --retries=3 --start-period=1s \
  CMD curl http://localhost/ || exit 1