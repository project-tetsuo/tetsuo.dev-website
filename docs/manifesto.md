# MANIFESTO

## Deploy code not containers

## What is this?

Welcome to Tetsuo.

Tetsuo is the brain child of some people who recognise that the future is code not containers.

To this end, we have written a facade API on top of [NGINX Unit](https://unit.nginx.org) to pull arbitrary code from Github onto a Unit server.

This is the first step in making a serverless platform that will eventually do the following things:

- Pull code from a Git repository
- Automatically update NGINX Unit configuration
- Apply the same codebase and configuration update to other Unit servers as part of a cluster (likely using [libp2p](https://codecowboy.io/development/libp2p/))

## Why Bother?

This is a good question. One of the drawbacks that we see with the current approach to serverless is the need to refactor code to enable it to work with most Function-as-a-Service platforms.  
This usually involves refactoring or wrapping code in some sort of eventing model, or making other changes to suit the proprietary serverless model.

When we first came across NGINX UNIT, we saw that the changes to code needed were minimal to none. Nothing to learn.

This made us think about what other components we would need to make this a reality.

....and Tetsuo was born.
