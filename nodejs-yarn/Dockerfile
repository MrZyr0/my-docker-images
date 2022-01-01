FROM alpine:latest AS builder
RUN apk add --update yarn nodejs-current
WORKDIR /app
COPY package*.json ./
RUN yarn install --frozen-lockfile --non-interactive --no-progress --production --pure-lockfile
COPY . .
EXPOSE 3000
CMD ["yarn", "start"]

FROM gcr.io/distroless/nodejs:16
COPY --from=build-env /app /app
WORKDIR /app
CMD ["index.js"]
