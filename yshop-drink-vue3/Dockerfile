# Stage 1: Build the application
FROM node:18 AS builder
WORKDIR /app
COPY package.json pnpm-lock.yaml ./
RUN npm install -g pnpm
RUN pnpm install
COPY . .
RUN pnpm run build:prod

# Stage 2: Serve with Nginx
FROM nginx:stable-alpine
COPY --from=builder /app/dist-prod /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
