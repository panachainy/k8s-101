FROM node:12.16.1-alpine

RUN yarn global add drakov@1.0.4

COPY ./mock mock

ENTRYPOINT ["drakov", "-f", "/mock/**/*.apib", "--public", "--watch", "--autoOptions", "--header", "Authorization", "--p", "3500"]
