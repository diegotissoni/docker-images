FROM alpine
MAINTAINER Franco Morinigo <franco.morinigo@almundo.com>

RUN apk --update add bash openssl

COPY freplace.sh freplace.sh

ENTRYPOINT ["./freplace.sh"]
