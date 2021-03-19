# 🥓 Lardons

**[strapi, mongo, nuxt, docker-compose]**
_"full stack framework"_ for the modern times

**This is absolutely not safe in any manner for production. Use only for local dev.**

## Overview
This is a docker-compose based stack that runs :
- [mongodb](https://github.com/mongodb/mongo) 
- [strapi](https://github.com/strapi/strapi) 
- [nuxt](https://github.com/nuxt/nuxt.js) 

Aimed at development only for now.
Start fullstacking in under 5 minutes with this boilerplate 🎉

## Usage
0. (**requirement**) latest `docker-compose` installed [github releases here](https://github.com/docker/compose/releases)
1. configure the `.env` variables
2. run `yarn start` or `npm start`
3. (_optional_) if you just cloned the repo, everything (strapi + mongo + nuxt) will be generated the first time you start the app, this takes a little time, check the progress out using `yarn logs`

## Commands
```bash
# YARN = NPM RUN

# all of these run OUTSIDE the CONTAINER
###################################################################
yarn start                          # docker-compose up -d
yarn logs                           # docker-compose logs -f
yarn shell                          # docker-compose exec node sh
yarn stop                           # docker-compose down

# all of these run INSIDE the CONTAINER
###################################################################
yarn client:add bootstrap@4.1.1     # npm install bootstrap
yarn client:restart                 # pm2 restart client
yarn client:logs                    # pm2 logs client
###################################################################
yarn server:strapi <command>        # strapi <command>          (broken see #2, exec manually inside the container)
yarn server:add graphql             # strapi install graphql    (broken see #2, exec manually inside the container)
yarn server:restart                 # pm2 restart server
yarn server:logs                    # pm2 logs server
```

## Architecture
1. dockerfile builds an image that has node, strapi, nuxt and pm2
2. this image has an entrypoint that checks if strapi or nuxt boilerplates are present
    1. if not, it installs them and automatically generates the boilerplates
    2. if yes, starts pm2 processes on the node container for client and server
3. this image is used on docker-compose with a mongo instance for the server

_(alot of behind the scenes magic is going on to have the correct permissions for linux development, your user needs to be in the docker group and you're set)_

## Other Resources
[inspired by this article](https://blog.strapi.io/cooking-a-deliveroo-clone-with-nuxt-vue-js-graphql-strapi-and-stripe-setup-part-1-7/), try following this guide to get a feel of what you can achieve using this stack in minutes.
