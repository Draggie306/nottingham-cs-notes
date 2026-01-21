
## Foreword
Before starting, it is important to understand what Workers are:
- They are serverless, meaning they do not run 24/7. Instead, when a request matches a URL that the Worker is configured to access, it spins up and runs the code. 
- You can specify which "routes" get responded to. For example, you may create an example that uses the domain, with `/map` to then access a map, or `/data` to get data. 
	- URLs can be decoded and parsed: you can include, for example, `/data?id=ab7c64fe` and get the data associated with the `id` parameter. This quickly becomes very powerful for creating whole account systems, authentication libraries, etc.
	- Workers can be fully RESTful, meaning you can send and respond with `GET`, `POST` JSON data, and more. 
- In a Worker, you can do pretty much anything. You can request another API (e.g. OpenAI's `responses`) and return the data as a response to the Worker's call. 

## Installing 
You can develop Workers fully locally but will need to deploy them on Cloudflare's network. Workers can be written in JavaScript, TypeScript or Python (in beta). Please let me know 

Follow this tutorial: https://developers.cloudflare.com/workers/wrangler/install-and-update/

> You will need to install Node.js and the npm package manger.

1. For local development of a Cloudflare Worker, we will use the Wrangler tool. Run the following in a new directory: `npx wrangler init` This will set up a basic worker to run. When doing this, select the "Hello World example", the Worker only (no SSR), and select either Javascript, TypeScript or Python.  

Once created, you can deploy on the Cloudflare network:
- Create a Cloudflare account, go to Workers and Pages and set up a new one: https://dash.cloudflare.com/?to=/:account/workers-and-pages

## Examples

A TypeScript worker will generally have the following structure:

```ts
export default {
	async fetch(request, env, ctx): Promise<Response> {
		return new Response('Hello World!');
	},
} satisfies ExportedHandler<Env>;
```

This means: at the subdomain the Worker is hosted on, or any route the Worker is configured to serve, it will return just the text "Hello World".

- My portfolio site uses a Worker, located on: https://github.com/Draggie306/portfolio/blob/main/worker.ts
- Here is an example of an old Worker of mine, which subrequests data from GitHub's API and serves them across a range of different URLs: https://github.com/Draggie306/CheatSheets/blob/main/cheatsheet-master.js

### Python

The equivalent to the Typescript worker above is the following:
```python
# entry.py
from workers import Response, WorkerEntrypoint
from submodule import get_hello_message
class Default(WorkerEntrypoint):
    async def fetch(self, request):
        return Response(get_hello_message())

# submodule.py
def get_hello_message():
    return "Hello World!"
```


## Deploying

Once you have created a Worker, signed in to an account, you can `npx wrangler dev` to run it locally. This will open a server and port on your local device which you can open in your browser to see what responses are returned. 

You can then `npx wrangler deploy` to run it on the Cloudflare network with a `workers.dev` subdomain. Anyone can access it!

Let me know if you have any issues.
