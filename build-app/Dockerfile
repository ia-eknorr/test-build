FROM myimage:latest

ENV MSG_APP="I came from the app!"

COPY entrypoint-shim.sh /entrypoint-shim.sh
RUN chmod +x /entrypoint-shim.sh

ENTRYPOINT ["/entrypoint-shim.sh"]