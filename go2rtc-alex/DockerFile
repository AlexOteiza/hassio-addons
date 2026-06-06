FROM docker:27-cli AS dockerfile_source

RUN apk add --no-cache git

RUN git clone --branch dev https://github.com/AlexOteiza/go2rtc.git /tmp/go2rtc


FROM ghcr.io/home-assistant/base:latest

RUN apk add --no-cache git go build-base ffmpeg ca-certificates tzdata

COPY --from=dockerfile_source /tmp/go2rtc /tmp/go2rtc

RUN cd /tmp/go2rtc \
 && go build -ldflags "-s -w" -o /usr/local/bin/go2rtc . \
 && chmod +x /usr/local/bin/go2rtc \
 && rm -rf /tmp/go2rtc

CMD ["/usr/local/bin/go2rtc", "-config", "/config/go2rtc.yaml"]
