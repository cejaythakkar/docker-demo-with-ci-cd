from node:20-alpine as builder

workdir /app

ARG VITE_API_URL=http://localhost:5555
ENV VITE_API_URL=$VITE_API_URL

copy package*.json ./

run npm install

copy . .
run npm run build

from nginx:alpine

copy nginx/default.conf /etc/nginx/conf.d/default.conf
copy --from=builder /app/dist /usr/share/nginx/html
expose 80
