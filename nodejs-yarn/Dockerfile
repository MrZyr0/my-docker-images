FROM alpine:latest AS builder
ENV NODE_ENV=production
WORKDIR /app
RUN apk update \
	&& apk add npm nodejs \
	&& rm -fr /var/cache/apk/*
COPY package*.json ./
RUN yarn install --frozen-lockfile --non-interactive --no-progress --production --pure-lockfile
COPY . .

FROM gcr.io/distroless/nodejs:16
COPY --from=builder /app /app
WORKDIR /app
CMD ["index.js"]
