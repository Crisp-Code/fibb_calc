# For Production Environment
FROM node:18-alpine as builder
USER node

RUN mkdir -p /home/node/app
WORKDIR '/home/node/app'

COPY --chown=node:node ./package.json ./
RUN npm install

RUN npm run build

COPY --chown=node:node ./ ./ 
CMD ["npm", "run", "start"]

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf 
COPY --from=builder /app/build /usr/share/nginx/html