FROM node:18-alpine

# Install confd and supervisord
RUN apk add --no-cache curl supervisor && \
    curl -L https://github.com/kelseyhightower/confd/releases/download/v0.16.0/confd-0.16.0-linux-amd64 -o /usr/local/bin/confd && \
    chmod +x /usr/local/bin/confd

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

# Create directories for confd
RUN mkdir -p /etc/confd/{conf.d,templates}

# Copy confd configs
COPY confd/ /etc/confd/

# Copy supervisord config
COPY supervisord.conf /app/supervisord.conf

EXPOSE 5000

# Use supervisord
CMD ["/usr/bin/supervisord", "-c", "/app/supervisord.conf"]