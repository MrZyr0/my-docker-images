FROM alpine:latest AS builder
RUN apk add --update npm nodejs-current
WORKDIR /app
COPY package*.json ./
RUN npm clean-install --only=production
COPY . .
EXPOSE 3000
CMD ["npm", "start"]

FROM gcr.io/distroless/nodejs:16
COPY --from=build-env /app /app
WORKDIR /app
CMD ["index.js"]
