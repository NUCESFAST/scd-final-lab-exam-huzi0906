# syntax=docker/dockerfile:1

ARG NODE_VERSION=16.13.0

FROM node:${NODE_VERSION}-alpine

ENV NODE_ENV production

WORKDIR /i211187_frontend

RUN --mount=type=bind,source=package.json,target=package.json \
    --mount=type=bind,source=package-lock.json,target=package-lock.json \
    --mount=type=cache,target=/root/.npm \
    npm ci --omit=dev

# Change ownership of the /i211187_frontend directory to the node user
RUN chown -R node:node /i211187_frontend

USER node

COPY . .

RUN npm run build

FROM nginx:alpine

COPY --from=0 /i211187_frontend/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]