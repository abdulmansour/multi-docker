FROM node:16-alpine as builder

WORKDIR /app

COPY package.json .
RUN npm install

COPY . .

# outputs static files inside /app/build
RUN npm run build

FROM nginx:alpine
# optional: expose 3000 is required for elasticbeanstalk to map to that port for incoming traffic
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
