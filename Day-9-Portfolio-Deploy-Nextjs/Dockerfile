FROM node:20-alpine AS builder

WORKDIR /portfolio-app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

FROM node:20-alpine

WORKDIR /portfolio-app

COPY --from=builder /portfolio-app/package*.json ./
COPY --from=builder /portfolio-app/node_modules ./node_modules
COPY --from=builder /portfolio-app/.next ./.next
COPY --from=builder /portfolio-app/public ./public

EXPOSE 3000

CMD ["npm", "start"]