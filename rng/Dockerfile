# Phase I - Builder source
FROM python:alpine as builder

WORKDIR /usr/src/app

COPY rng.py ./
COPY requirements.txt ./
COPY pylint.cfg ./

WORKDIR /wheels

RUN cp /usr/src/app/requirements.txt ./
RUN pip wheel -r ./requirements.txt 

# Phase II - Lints Code 
FROM eeacms/pylint:latest as linting
WORKDIR /code
COPY --from=builder /usr/src/app/pylint.cfg /etc/pylint.cfg
COPY --from=builder /usr/src/app/rng.py ./
RUN ["/docker-entrypoint.sh", "pylint"]

# Phase III - Final Image 
FROM python:alpine as serve
WORKDIR /usr/src/app
# Copy all packages instead of rerunning pip install
COPY --from=builder /wheels /wheels
RUN     pip install -r /wheels/requirements.txt \
                      -f /wheels \
       && rm -rf /wheels \
       && rm -rf /root/.cache/pip/* 

COPY --from=builder /usr/src/app/*.py ./
EXPOSE 80
CMD ["python", "rng.py"]

