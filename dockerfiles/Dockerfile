FROM alpine:3.4
MAINTAINER Gibson Fahnestock "gib@fahn.co"

COPY cobalt /usr/bin/cobalt
RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2
EXPOSE 3000
CMD ["/usr/bin/cobalt"]
