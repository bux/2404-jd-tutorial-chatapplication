# build image
FROM node:20-alpine AS build
WORKDIR /source

RUN npm install -g pnpm

COPY package.json pnpm-lock.yaml ./

RUN pnpm install

COPY . .

RUN pnpm build


# final stage/image
FROM nginx:alpine

COPY --from=build /source/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
