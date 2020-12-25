FROM node:12.18.1-alpine as intermediate
LABEL stage=builder
RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh

# Initiate the key
ARG ACCESS_KEY
RUN mkdir /root/.ssh/
RUN echo "${ACCESS_KEY}" > /root/.ssh/id_rsa
RUN chmod 600 /root/.ssh/id_rsa
RUN chmod 755 /root/.ssh/
RUN touch /root/.ssh/known_hosts
RUN ssh-keyscan github.com >> /root/.ssh/known_hosts

# Perform package installation
WORKDIR /app
COPY package*.json ./
RUN npm install

# Second stage image
FROM node:12.18.1-alpine
WORKDIR /app
COPY --from=intermediate /app /app
COPY . .
CMD ["npm", "start"]
