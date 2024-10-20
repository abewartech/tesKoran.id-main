FROM node:20-slim as base

ARG NEXT_PUBLIC_API_URL

WORKDIR /app

RUN useradd -ms /bin/sh -u 1001 app
USER root
COPY --chown=app:app /apps/frontend/package*.json ./
RUN npm install
USER root
RUN mkdir -p /app/.next/cache/eslint && chmod -R 777 /app/.next

COPY --chown=app:app /apps/frontend/ /app/

FROM base as prod
RUN npm run build
CMD ["npm", "start", "3000"]

FROM base as dev
CMD ["npm", "run", "dev"]
