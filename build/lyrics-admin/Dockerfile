FROM node:20-alpine

# 1. Install Git
RUN apk add --no-cache git

WORKDIR /app

# 2. Accept the repo argument from docker-compose
ARG LYRICS_ADMIN_REPO
RUN if [ -z "$LYRICS_ADMIN_REPO" ]; then echo "Build argument LYRICS_ADMIN_REPO is required" && exit 1; fi

# 3. Clone the repo directly into the current folder
RUN git clone ${LYRICS_ADMIN_REPO} .

# 4. Install dependencies and Build
# We use 'npm install' instead of 'ci' to be more forgiving if lockfiles are missing
RUN npm install
RUN npm run build

# 5. Start the app
EXPOSE 7150
ENV PORT=7150
CMD ["npm", "start"]