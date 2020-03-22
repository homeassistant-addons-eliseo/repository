FROM ubuntu:18.04

RUN apt-get update \
    \
    && apt-get install -y --no-install-recommends \
        build-essential=12.4ubuntu1 \
        cargo=0.40.0-3ubuntu1~18.04.1 \
        git=1:2.17.1-1ubuntu0.5 \
        libasound2-data=1.1.3-5ubuntu0.2 \
        libasound2-dev=1.1.3-5ubuntu0.2 \
        libasound2-plugins=1.1.1-1ubuntu1 \
        libasound2=1.1.3-5ubuntu0.2 \
        libssl-dev=1.1.1-1ubuntu2.1~18.04.5 \
        pkg-config=0.29.1-0ubuntu2 \
        rustc=1.39.0+dfsg1+llvm-3ubuntu1~18.04.1 \
    \
    && git clone --branch "v0.2.23" --depth=1 \
        https://github.com/Spotifyd/spotifyd.git /tmp/spotifyd \
    \
    && cd /tmp/spotifyd \
    && cargo build --release \
    && mv /tmp/spotifyd/target/release/spotifyd /usr/bin \
    \
    && apt-get purge -y --auto-remove \
        build-essential \
        cargo \
        git \
        libasound2-dev \
        libssl-dev \
        pkg-config \
        rustc \
    \
    && rm -fr \
        /tmp/* \
        /root/.cargo \
        /var/{cache,log}/* \
        /var/lib/apt/lists/*

CMD ["mkdir -p /share/spotify && spotifyd --no-daemon --backend pipe > /share/spotify/fifo"]
