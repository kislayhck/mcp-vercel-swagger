# Example Next.js MCP Server

**Uses `mcp-handler`**

## Usage

This sample app uses the [Vercel MCP Adapter](https://www.npmjs.com/package/mcp-handler) that allows you to drop in an MCP server on a group of routes in any Next.js project.

Update `app/mcp/route.ts` with your tools, prompts, and resources following the [MCP TypeScript SDK documentation](https://github.com/modelcontextprotocol/typescript-sdk/tree/main?tab=readme-ov-file#server).

> **Note:** This implementation uses a single route at `/mcp` that supports both SSE and HTTP transports. Some templates use dynamic routing like `app/[transport]/route.ts` to separate transports into different routes (e.g., `/sse`, `/stdio`), but `mcp-handler` handles both on the same route.

## Features

This implementation includes three powerful tools:

- **load-swagger**: Load and inspect Swagger/OpenAPI specifications from HTTPS URLs
- **login**: Authenticate with APIs and retrieve authentication tokens
- **call-api**: Make authenticated API calls to any endpoint

## Notes for running on Vercel

- To use the SSE transport, requires a Redis attached to the project under `process.env.REDIS_URL` and toggling the `disableSse` flag to `false` in `app/mcp/route.ts`
- Make sure you have [Fluid compute](https://vercel.com/docs/functions/fluid-compute) enabled for efficient execution
- After enabling Fluid compute, open `app/mcp/route.ts` and adjust `maxDuration` to 800 if you are using a Vercel Pro or Enterprise account
- [Deploy the Next.js MCP template](https://vercel.com/templates/next.js/model-context-protocol-mcp-with-next-js)

## Sample Client

`scripts/test-client.mjs` contains a sample client to try invocations via SSE transport:

```sh
node scripts/test-client.mjs http://localhost:3000
```

Or use the HTTP transport with `scripts/test-streamable-http-client.mjs`:

```sh
node scripts/test-streamable-http-client.mjs http://localhost:3000
```
