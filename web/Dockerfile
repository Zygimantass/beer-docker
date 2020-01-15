FROM node:13.6.0-alpine3.10 AS build-env
ARG BACKEND_IP 

RUN apk --no-cache add build-base git bzr gcc
RUN git clone https://github.com/Zygimantass/beer-frontend /src/beer-frontend
ENV REACT_APP_BACKEND_IP ${BACKEND_IP}
ENV PATH /src/beer-frontend/node_modules/.bin:$PATH
WORKDIR /src/beer-frontend/
RUN npm install --silent
RUN npm install react-scripts@3.0.1 -g --silent
RUN npm run build

FROM nginx:1.16.0-alpine
COPY --from=build-env /src/beer-frontend/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
