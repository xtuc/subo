FROM suborbital/subo:dev as subo

FROM ghcr.io/grain-lang/grain:0.4-slim

WORKDIR /root
RUN mkdir runnable; mkdir suborbital

COPY --from=subo /go/bin/subo /usr/local/bin

WORKDIR /root/runnable