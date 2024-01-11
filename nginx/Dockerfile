FROM node

WORKDIR /app

EXPOSE 3000

COPY package.json package-lock.json ./

RUN npm i

COPY . ./

CMD ["npm", "start"]
