FROM alpine:3.13.2

ENV MSG_BASE="I am an environment variable from the base image!"
ENV MSG_BASE_OVERRIDE="I am an environment variable from the base image, but I can be overridden by the app image!"

COPY entrypoint-shim.sh /entrypoint-shim.sh
RUN chmod +x /entrypoint-shim.sh

ENTRYPOINT ["/entrypoint-shim.sh"]