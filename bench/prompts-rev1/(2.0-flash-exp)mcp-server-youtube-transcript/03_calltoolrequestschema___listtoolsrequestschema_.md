# Chapter 3: CallToolRequestSchema & ListToolsRequestSchema

This chapter focuses on the `CallToolRequestSchema` and `ListToolsRequestSchema`, which are crucial for defining the structure of requests that the MCP server accepts. These schemas ensure that incoming requests are valid and can be processed correctly. They are used by the MCP server (introduced in the [`Model Context Protocol (MCP) Server`](01_model_context_protocol__mcp__server_.md) chapter) to validate and route incoming requests.

## CallToolRequestSchema

The `CallToolRequestSchema` defines the structure for requesting the execution of a specific tool. It includes the name of the tool to be called and any arguments required by that tool.

Here's a simplified representation of the schema:

```typescript
interface CallToolRequest {
  method: "callTool";
  params: {
    name: string;
    arguments?: Record<string, any>;
  };
}
```

Breaking down the `CallToolRequestSchema`:

*   `method: "callTool"`:  Specifies that this request is intended to call a specific tool.  This is a constant value.
*   `params`:  Contains the parameters for the tool call.
    *   `name: string`: The name of the tool to be executed (e.g., `"get_transcript"` as defined in the [`get_transcript` Tool](02__get_transcript__tool_.md) chapter).
    *   `arguments?: Record<string, any>`: An optional object containing the arguments to be passed to the tool. The keys of the object are the argument names, and the values are the argument values.  The type `Record<string, any>` indicates a dictionary where keys are strings, and values can be of any type.

For example, a valid `CallToolRequest` to execute the `get_transcript` tool might look like this:

```json
{
  "method": "callTool",
  "params": {
    "name": "get_transcript",
    "arguments": {
      "url": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
      "lang": "en"
    }
  }
}
```

In this example, the `name` is set to `"get_transcript"`, and the `arguments` object contains the `url` and `lang` parameters required by the `get_transcript` tool.

If the `lang` argument is not provided, the request would look like this:

```json
{
  "method": "callTool",
  "params": {
    "name": "get_transcript",
    "arguments": {
      "url": "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
    }
  }
}
```

Or even:

```json
{
  "method": "callTool",
  "params": {
    "name": "get_transcript",
    "arguments": {
      "url": "dQw4w9WgXcQ"
    }
  }
}
```

## ListToolsRequestSchema

The `ListToolsRequestSchema` defines the structure for requesting a list of available tools from the server. It is a much simpler schema compared to `CallToolRequestSchema`.

Here's a simplified representation:

```typescript
interface ListToolsRequest {
  method: "listTools";
}
```

Breaking down the `ListToolsRequestSchema`:

*   `method: "listTools"`: Specifies that this request is intended to retrieve a list of available tools. This is a constant value.

A valid `ListToolsRequest` would simply be:

```json
{
  "method": "listTools"
}
```

When the MCP server receives a request matching this schema, it responds with a list of available tools, as defined by the `TOOLS` constant in the `TranscriptServer` class (introduced in the [`Model Context Protocol (MCP) Server`](01_model_context_protocol__mcp__server_.md) chapter).

## Usage in the Server

As shown in the [`Model Context Protocol (MCP) Server`](01_model_context_protocol__mcp__server_.md) chapter, the `TranscriptServer` uses these schemas to handle incoming requests:

```typescript
this.server.setRequestHandler(ListToolsRequestSchema, async () => ({
  tools: TOOLS
}));

this.server.setRequestHandler(CallToolRequestSchema, async (request) => 
  this.handleToolCall(request.params.name, request.params.arguments ?? {})
);
```

The `setRequestHandler` method associates each schema with a corresponding handler function. When a request is received, the server checks its `method` and validates it against the registered schemas. If the request matches a schema, the associated handler function is called. This mechanism ensures that only valid requests are processed by the server.  Invalid requests will result in an error, described in the [`McpError`](07_mcperror_.md) chapter.

## Summary

In this chapter, we explored the `CallToolRequestSchema` and `ListToolsRequestSchema`, which define the structure of requests accepted by the MCP server. The `CallToolRequestSchema` specifies the format for requesting a specific tool to be executed, while the `ListToolsRequestSchema` specifies the format for requesting a list of available tools. These schemas are essential for ensuring that requests are valid and can be processed correctly by the server.

Next, we'll delve into the [`YouTubeTranscriptExtractor`](04_youtubetranscriptextractor_.md), which is responsible for the actual extraction of transcripts from YouTube videos.


---

Generated by [AI Codebase Knowledge Builder](https://github.com/The-Pocket/Tutorial-Codebase-Knowledge)