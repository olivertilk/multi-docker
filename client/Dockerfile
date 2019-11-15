### Build phase
FROM node:alpine AS builder
WORKDIR '/app'
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

### Run phase
# 'FROM' starts a new block
FROM nginx
# This command doesn't do anything locally but is used by Elastic Beanstalk to expose port 80 to the outside world
EXPOSE 3000
# Copy nginx default.conf file over to change the port nginx listens on
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# Copy the production build to the nginx public facing folder
COPY --from=builder /app/build /usr/share/nginx/html