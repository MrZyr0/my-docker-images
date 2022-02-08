FROM alpine:latest AS ts-builder
ENV NODE_ENV=production
WORKDIR /app
RUN apk update \
	&& apk add npm nodejs \
	&& rm -fr /var/cache/apk/*
COPY package*.json ./
COPY tsconfig*.json ./
RUN npm ci
COPY . .
CMD ["npm", "run", "build"]

FROM alpine:latest AS app-builder
ENV NODE_ENV=production
WORKDIR /app
RUN apk update \
	&& apk add npm nodejs \
	&& rm -fr /var/cache/apk/*
COPY --from=ts-builder /app/package*.json ./
RUN npm ci
COPY --from=ts-builder /app ./

FROM gcr.io/distroless/nodejs:16
WORKDIR /app
COPY --from=app-builder /app ./
USER 1000
CMD ["index.js"]
