FROM node:20-alpine

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

EXPOSE 3000

# Important: Update this to specify the host
ENV HOSTNAME "0.0.0.0"

# Use this command instead of npm start
CMD ["npm", "run", "start", "--", "-H", "0.0.0.0"]
