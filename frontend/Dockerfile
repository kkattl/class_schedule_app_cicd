FROM --platform=linux/amd64 node:14-alpine AS build-stage
COPY ./frontend /frontend
WORKDIR /frontend

ARG REACT_APP_API_BASE_URL
ENV REACT_APP_API_BASE_URL=$REACT_APP_API_BASE_URL

RUN npm install
RUN npm run build

FROM --platform=linux/amd64 nginx:alpine AS production-stage
RUN rm -rf /usr/share/nginx/html
WORKDIR /usr/share/nginx/html
COPY --from=build-stage /frontend/build .
COPY nginx.conf /etc/nginx/nginx.conf
CMD ["nginx", "-g", "daemon off;", "-c", "/etc/nginx/nginx.conf"]