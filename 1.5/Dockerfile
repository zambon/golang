FROM ppc64le/golang:1.8.2

ENV GOLANG_VERSION 1.5.2
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz
ENV GOLANG_DOWNLOAD_SHA1 c7d78ba4df574b5f9a9bb5d17505f40c4d89b81c

RUN set -x && \
	mv /usr/local/go /usr/local/go182 && \
	curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz && \
	echo "$GOLANG_DOWNLOAD_SHA1  golang.tar.gz" | sha1sum -c - && \
	tar -C /usr/local -xzf golang.tar.gz && \
	rm golang.tar.gz && \
	cd /usr/local/go/src && \
	GOROOT_BOOTSTRAP=/usr/local/go182 ./make.bash && \
	rm -rf /usr/local/go182

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

COPY go-wrapper /usr/local/bin/
