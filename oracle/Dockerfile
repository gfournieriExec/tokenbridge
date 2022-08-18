FROM node:10

RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y libc6-dev
# RUN apt-get install -y libc6-dev-i386
RUN git config --global url.https://github.com/.insteadOf git://github.com/

RUN apt-get install -y wget
RUN apt-get clean

WORKDIR /mono
COPY package.json .
COPY commons/package.json ./commons/
COPY oracle/package.json ./oracle/
COPY yarn.lock .
RUN yarn install --production --frozen-lockfile

COPY ./contracts ./contracts
RUN cd ./contracts; npm install;npm run compile; cd ..

RUN mv ./contracts/build ./ && rm -rf ./contracts/* ./contracts/.[!.]* && mv ./build ./contracts/

COPY ./commons ./commons

COPY ./oracle ./oracle
WORKDIR /mono/oracle
CMD echo "To start a bridge process run:" \
  "VALIDATOR_ADDRESS=<validator address> VALIDATOR_ADDRESS_PRIVATE_KEY=<validator address private key> docker-compose up -d --build"
