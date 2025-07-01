# Use official Node.js LTS image
FROM node:20

# Install pnpm and turbo globally
RUN npm install -g pnpm@9.14.2 turbo@2.3.1

# Set workdir to monorepo root
WORKDIR /app

# Copy everything
COPY . .

# Set up pnpm config (optional)
RUN pnpm config set store-dir ~/.pnpm-store

# Install dependencies for entire monorepo
RUN pnpm install --frozen-lockfile

# Turbo prune (optional: keeps only necessary packages, fastest and smallest images)
RUN turbo prune --scope=@kan/web --scope=@kan/db --docker

# Build the web app
RUN pnpm --filter @kan/web build

# Set working directory to web app for runtime
WORKDIR /app/apps/web

# Expose port 3000
EXPOSE 3000

# Start the app
CMD ["pnpm", "start"]
