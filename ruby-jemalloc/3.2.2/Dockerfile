FROM ruby:3.2.2-slim-bookworm

RUN apt-get update && apt-get install -y -qq \
      build-essential \
      libpq-dev \
      libjemalloc2 \
      libjemalloc-dev \
      --no-install-recommends \
      --fix-missing

ENV LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libjemalloc.so.2
