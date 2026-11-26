<p align="left"><img src="logo.svg" alt="Underwriters Technologies" height="48"></p>

# Underwriters Technologies free tools: MCP server

A free, public MCP server for insurance underwriting lookups in the United States.
It needs no key and no sign-in. Every tool only reads data.

- Endpoint: `https://toolsapi.undtec.com/mcp`
- Transport: Streamable HTTP
- MCP Registry name: `com.undtec/tools`
- Web pages of the tools: https://www.undtec.com/tools/

## Tools

| Tool | What it returns | Data source | Web page |
|---|---|---|---|
| `tools_overview` | Every tool, its data source and its web page. Call it first. | - | https://www.undtec.com/tools/ |
| `geocode_address` | Latitude and longitude of a US street address. | US Census Geocoder | https://mappin.undtec.com/ |
| `get_wildfire_hazard` | Wildfire Hazard Potential class and wildland-urban interface (WUI) class at a point. | USFS WHP 2023, SILVIS/USFS WUI 2020 | https://wildfire.undtec.com/ |
| `get_flood_zone` | FEMA flood zone at a point, its subtype, and whether it is a Special Flood Hazard Area. | FEMA National Flood Hazard Layer | https://flood.undtec.com/ |
| `get_distance_to_coast` | Miles from a point to the nearest coastline, and the nearest coast point. | Underwriters Technologies coastline models, NOAA, OpenStreetMap, GSHHG | https://dtc.undtec.com/ |
| `decode_vin` | Year, make, model, trim, body, engine and plant of a vehicle. | NHTSA vPIC | https://vin.undtec.com/ |
| `lookup_fmcsa_carrier` | FMCSA status, safety rating, authority and insurance filings of a motor carrier. | FMCSA | https://fmcsa.undtec.com/ |
| `search_insurance_carriers` | US insurance companies that match a name. | NAIC registry | https://carriers.undtec.com/ |
| `get_insurance_carrier` | One US insurance company by NAIC code. | NAIC registry | https://carriers.undtec.com/ |
| `get_surplus_lines_tax_rates` | Surplus lines tax rate and fees of a US state. | State insurance departments | https://sltax.undtec.com/ |

Each answer gives its data source and a link to the web page that shows the same result.

## One server per tool

Each tool site also has its own MCP server with only its own tools:

| Server | Endpoint | MCP Registry name |
|---|---|---|
| Wildfire Map | `https://wildfire.undtec.com/mcp` | `com.undtec/wildfire` |
| FloodMap | `https://flood.undtec.com/mcp` | `com.undtec/flood` |
| Distance to Coast | `https://dtc.undtec.com/mcp` | `com.undtec/dtc` |
| Longitude-Latitude Finder | `https://mappin.undtec.com/mcp` | `com.undtec/mappin` |
| VIN Decoder | `https://vin.undtec.com/mcp` | `com.undtec/vin` |
| FMCSA Carrier Lookup | `https://fmcsa.undtec.com/mcp` | `com.undtec/fmcsa` |
| Carrier Lookup | `https://carriers.undtec.com/mcp` | `com.undtec/carriers` |
| Surplus Lines Tax Calculator | `https://sltax.undtec.com/mcp` | `com.undtec/sltax` |

## Connect

Claude Code:

```
claude mcp add --transport http undtec-tools https://toolsapi.undtec.com/mcp
```

Claude Desktop, Cursor, VS Code and other clients (JSON configuration):

```json
{
  "mcpServers": {
    "undtec-tools": {
      "type": "http",
      "url": "https://toolsapi.undtec.com/mcp"
    }
  }
}
```

Claude.ai: Settings, Connectors, Add custom connector, then paste `https://toolsapi.undtec.com/mcp`.

## Example questions

- "What is the wildfire hazard and the flood zone at 1600 Amphitheatre Parkway, Mountain View, CA?"
- "How far is 123 Ocean Drive, Miami Beach, FL from the coast?"
- "Look up this USDOT number and tell me its insurance filings: <your USDOT number>."
- "What is the surplus lines tax rate in Texas?"

## Limits

- The results are screening information. They are not an inspection, an official flood zone determination,
  a loss estimate or a coverage decision.
- Rate limit: 30 requests a minute for each IP address.
- Each data source call stops after 8 seconds.
- The server stores nothing that you send.

## About this repository

This repository holds the listing of the server: this README, `server.json` and the logo.
The server source code is private. To report a problem, open an issue here.

Made by Underwriters Technologies, https://www.undtec.com/
