From node:20-alpine as builder
WORKDIR /app
COPY package*.json ./
run npm install
copy . .
run npm run build

From node:20-alpine as runtime

workdir /app
COPY --from=builder /app/package*.json ./
run npm install --omit=dev
copy --from=builder /app/dist ./dist
expose 5555
cmd ["node","dist/server.js"]
