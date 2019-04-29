FROM python:3.7-alpine as base
FROM base as builder

RUN mkdir /install
WORKDIR /install

COPY requirements.txt /requirements.txt

RUN pip install --install-option="--prefix=/install" -r /requirements.txt

FROM base

EXPOSE 3000
COPY --from=builder /install /usr/local
COPY server.py  /app/server.py
WORKDIR /app

CMD gunicorn --log-level warning --bind 0.0.0.0:3000 --reuse-port --workers $(nproc) --worker-class gunicorn.workers.gtornado.TornadoWorker server:app
