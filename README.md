![](https://nextwork.ai/mos-dev/uploads/02a35a5b-1d8b-43ee-9982-6ceef44145e5_kqswhxb2)

## Project Overview

### What we're building and why

In this project, I'm building a URL shortener so that I can learn and practically implement tools Docker, PostgreSQL and Redis.

## Setting Up the Environment

### Environment setup goals

In this step, I'm setting up Docker so that I can have the ability to run my services as containers.

![Setting Up the Environment](https://nextwork.ai/mos-dev/uploads/02a35a5b-1d8b-43ee-9982-6ceef44145e5_qj4lc3tb)

### The three core services

The three services are an API service, a database and cache. The first handles receiving and routing of incomin requests. The second stores the URL  . The third provides access to frequently accessed URL mappings by storing them in memory.

## Designing the System Architecture

### Architecture design goals

In this step, I'm creating the infrastructure files so that I can define how the services are started, built andconnected.

![Designing the System Architecture](https://nextwork.ai/mos-dev/uploads/02a35a5b-1d8b-43ee-9982-6ceef44145e5_pnungqem)

### Services defined in docker-compose.yml

The three services are web, database and redis. Each one handles a specific function.Web is for the python API server.The database stores the URL's. Redis keeps frequently acessed URL mappings in memory.

![Designing the System Architecture](https://nextwork.ai/mos-dev/uploads/02a35a5b-1d8b-43ee-9982-6ceef44145e5_ymp8agg2)

### Infrastructure file deep dive

I chose requirements.txt . Its role is to provide docker with the prerequisites for it to build the app.

## Building the URL Shortener Logic

### Application logic goals

In this step, I'm writing the app.py file. This file will handle both converting long URL's to short codes and redirecting the short codes back to the original URL.

### The URL shortening flow

When a long URL hits /shorten, the app first checks to make sure the URL is legit, then it assigns the URL a unque short code and finally returns a ticket that redirects you to the base URL.

![Building the URL Shortener Logic](https://nextwork.ai/mos-dev/uploads/02a35a5b-1d8b-43ee-9982-6ceef44145e5_seusouy2)

### Handling redirect lookups

When someone visits a short URL, the app first checks redis; the cache memory. If that misses, it falls back to the PostgreSQL and caches the result for next time and issues a 302 redirect.

## Launching and Verifying the System

### Launch goals

In this step, I'm starting by using docker compose so that I can build my flask image, pull the database.

![Launching and Verifying the System](https://nextwork.ai/mos-dev/uploads/02a35a5b-1d8b-43ee-9982-6ceef44145e5_3w4aoken)

### Health endpoint response

When I ran curl I got an error so i used "Invoke-RestMethod -Uri http://localhost:5000/health"

## Testing and Observing the System

### Testing goals

In this step, I'm testing how the redirects work so that I can observe the redis caching layer in real time.

### Redis cache flush behavior

After flushing Redis, the app had to query the database instead of retrieving it from the cache memory and then re-write the short URL mapping onto redis cache.

## Implementing Rate Limiting with Redis

![Implementing Rate Limiting with Redis](https://nextwork.ai/mos-dev/uploads/02a35a5b-1d8b-43ee-9982-6ceef44145e5_i71om2um)

### Why Redis excels at rate limiting

In this project extension, Redis is better for rate limiting because it is faster whereas storing counters in PostgreSQL is much slower and would slow the system down which leads to excessive use of resources.

## Reflections and Key Takeaways

### Tools and concepts learned

The key tools I used include docker, redis, PostgreSQL and Python. Key concepts I learnt include memory caching, PostgreSQL for databases and even rate limiting.

### Time and challenges

This project took me approximately 3 hours.The most challenging part was. carrying out te tests.

### Final thoughts

I did this project today to learn how to use docker and implement containerization in my own projects. Another skill I want to learn is Kubernetes.
