FROM alpine:latest AS unzipper
RUN apk add --no-cache wget unzip
RUN mkdir /tmp/playlists && \
  wget -O /tmp/hitster-youtube-playlists.zip https://github.com/andygruber/songseeker-hitster-playlists/archive/refs/tags/v2.0.1.zip && \
  unzip /tmp/hitster-youtube-playlists.zip -d /tmp/playlists/

FROM nginx
COPY imagebuild/default.conf /etc/nginx/conf.d/default.conf

RUN rm -rf /usr/share/nginx/html/*
COPY *.js *.json *.csv *.html *.css *.png icons/* /usr/share/nginx/html/
RUN mkdir -m 755 -p /usr/share/nginx/html/playlists
COPY --from=unzipper /tmp/playlists/ /usr/share/nginx/html/playlists/
RUN chmod 444 /usr/share/nginx/html/playlists/*
