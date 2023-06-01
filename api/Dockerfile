FROM debian:latest

RUN apt update
RUN apt install curl build-essential git python3 python3-pip -y

SHELL ["/bin/bash", "--login", "-c"]

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

WORKDIR /app/ZeppelinBot
ARG GIT_REPO=https://github.com/Dragory/ZeppelinBot.git
RUN git clone $GIT_REPO .

RUN nvm install

WORKDIR /app/ZeppelinBot/backend
RUN npm i
RUN npm run build

ARG DB_DATABASE
ARG DB_PASSWORD
ARG DB_PORT
ARG DB_USER
ARG DB_HOST
ARG DASHBOARD_URL
ARG API_URL
ARG KEY
ARG STAFF
ARG DASHBOARD_URL
ARG CLIENT_SECRET
ARG CLIENT_ID
ARG BOT_TOKEN
ARG DEFAULT_ALLOWED_SERVERS
ARG API_PORT=3000

RUN npm run migrate-prod

ENTRYPOINT ["/bin/bash", "--login", "-c", "npm run start-api-prod"]
