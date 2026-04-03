# MCP Weather Connector

A simple Model Context Protocol (MCP) server that connects Claude to real-time weather data using external APIs.

## Overview

This project demonstrates how to build and integrate a custom MCP server with Claude.
The server exposes tools that allow Claude to fetch weather forecasts and alerts dynamically instead of relying on its internal knowledge.

The goal of this project was to understand:

* How MCP servers work
* How tools are exposed to LLMs
* How external APIs can be integrated into AI workflows

## Features

* Fetch weather forecast using latitude and longitude
* Retrieve active weather alerts for a given region
* Async API handling using `httpx`
* Clean formatting of weather data for readable responses

## Tools Implemented

### 1. `get_forecast`

Returns weather forecast for a given location.

**Inputs:**

* latitude
* longitude

---

### 2. `get_alerts`

Returns active weather alerts for a region.

**Input:**

* state (US state code)

---

## Tech Stack

* Python
* MCP (Model Context Protocol)
* FastMCP
* httpx (for API requests)

## How It Works

1. The MCP server runs locally using STDIO transport.
2. Claude connects to the server via configuration.
3. When a relevant query is asked:

   * Claude calls the appropriate tool
   * The server fetches data from the weather API
   * The formatted response is returned to Claude

## Setup

1. Install dependencies:

   ```bash
   uv add "mcp[cli]" httpx
   ```

2. Run the server:

   ```bash
   uv run weather.py
   ```

3. Add server config in Claude:

   * Update `claude_desktop_config.json`
   * Provide the correct path to your project

4. Restart Claude Desktop

## Demo

![Demo Screenshot](https://github.com/RummanShuja/mcp-weather-connector/blob/aa1d79e0fd20b225a7dea7a80fda3d3eb7221df6/assets/img1.png)
![Demo Screenshot](https://github.com/RummanShuja/mcp-weather-connector/blob/aa1d79e0fd20b225a7dea7a80fda3d3eb7221df6/assets/img2.png)

## Notes

* This project currently uses the National Weather Service API, which supports only US locations.
* Tool usage depends on Claude’s decision-making (it may not always call the tool unless required).

## Learning Outcome

Through this project, I learned:

* How LLMs interact with external tools
* Importance of tool descriptions in MCP
* How to debug tool-calling behavior
* Limitations of relying on public APIs

## Future Improvements

* Support global weather APIs (e.g., OpenWeatherMap)
* Add caching for faster responses
* Improve tool descriptions to enforce usage
* Build a UI around the MCP server

---

## Reference

Based on concepts from MCP documentation and experimentation with Claude integration. 
