FROM node:8
RUN git config --global url.https://github.com/.insteadOf git://github.com/

WORKDIR /mono
COPY package.json .

COPY commons/package.json ./commons/
COPY ui/package.json ./ui/
COPY ui/lib/web3-eth/index.js ./ui/lib/web3-eth/index.js
COPY yarn.lock .
RUN yarn install --production --frozen-lockfile

COPY ./contracts ./contracts

RUN cd ./contracts; npm install;npm run compile; cd ..
RUN mv ./contracts/build ./ && rm -rf ./contracts/* ./contracts/.[!.]* && mv ./build ./contracts/

COPY ./commons ./commons
COPY ./ui ./ui
WORKDIR /mono/ui
CMD echo "To start a UI application run:" \
  "yarn start"
