
### STAGE 1: Build ###

# We label our stage as 'builder'
FROM node:12-alpine as builder

WORKDIR /ng-app

COPY package.json ./

RUN npm set progress=false && npm config set depth 0 && npm cache clean --force

## Storing node modules on a separate layer will prevent unnecessary npm installs at each build
RUN npm i
RUN npm run clean
COPY . .
RUN npm run build
## Build the angular app in production mode and store the artifacts in dist folder

# ### STAGE 2: Setup ###
#FROM nginx:1.17.3-alpine

# ## Remove nginx default conf
# RUN rm /etc/nginx/conf.d/default.conf

# ## Remove default nginx website
# RUN rm -rf /usr/share/nginx/html/*

# ## From 'builder' stage copy over the artifacts in dist folder to default nginx public folder
# COPY --from=builder ./ng-app/dist/cerbotDemoapp /usr/share/nginx/html

# ## Copy our default nginx config
# COPY --from=builder ./ng-app/nginx/default.conf /etc/nginx/sites-available/
# RUN ln -s /etc/nginx/sites-available/default.conf /etc/nginx/conf.d/
# RUN nginx -t
# CMD ["nginx", "-g", "daemon off;"]