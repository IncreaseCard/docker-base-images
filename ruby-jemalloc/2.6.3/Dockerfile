FROM ruby:2.6.3-slim-stretch

RUN apt-get update && apt-get install -y -qq \
      build-essential \
      libpq-dev \
      libjemalloc-dev \
      --no-install-recommends \
      --fix-missing

ENV LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libjemalloc.so.1
