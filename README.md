# Listing Location Toolkit (Remote MCP Server)

**Location facts for property and business-for-sale listings, written ready to paste, with sources.** Give it an address in the US or UK and it answers the questions buyers ask: how far to the nearest town, cities and airports, how many people live within a 1, 2 or 4 hour drive, what lakes, coast, mountains, national parks and attractions are nearby, whether the site is on the water, how big the plot is, and where to get an aerial photo.

For home buyers it also answers the family questions: which schools are nearby and how they are rated, which school district the address is in, how far the supermarket, doctor, station and playground are, whether daily needs are within a 15 minute walk, what the neighbourhood earns and what homes sell for, the flood zone, and street crime.

Built for AI agents working for estate agents, business brokers, home buyers and their teams. No install, no API key, no signup. Connect by URL and call it.

```
https://listing-location-toolkit.nerolabs.workers.dev/mcp
```

Free to use during launch.

## Why it exists

Map APIs hand back raw numbers. A listing needs sentences like "About 1.9 million people live within a 2 hour drive" with a source a buyer's adviser can check. The people count is the hard part: public drive-time services stop at 60 minutes, and a drive-time population report from the big analytics vendors costs about $50 each. This server does it in one call for the US and UK.

## Tools

| Tool | What it does |
|---|---|
| `listing_location_pack` | Everything for one address in one call: drive times, people within 1, 2 and 4 hours, nearby nature and attractions, waterfront and national park checks, mapped site size, map links, `listing_lines` to paste, and sources. 10 to 25 seconds. |
| `home_buyer_report` | Everything a home buyer asks in one call: schools, everyday places and the 15 minute walk check, the neighbourhood, flood zone and crime, with `listing_lines` and sources. 10 to 25 seconds. |
| `schools_nearby` | Nearest primary, middle, secondary, private, special and nursery schools with miles, walk and drive minutes. England: the DfE register with the latest Ofsted grade or report card, pupils, faith and selective flag. US: every public school (NCES 2024-25, pupils per teacher, free lunch share) and private schools, the school district the address is in, and the schools that district runs. Explains who sets catchments. |
| `daily_needs` | Supermarket, corner shop, doctor, pharmacy, dentist, hospital, station, bus stop, EV charger, playground, park, childcare, library, sports centre, gym, cafe, pub and more: the nearest of each with walk minutes, how many are within a 15 minute walk, and a walk score out of 7. |
| `area_profile` | US: census tract income, home value, rent, age, owners, households with children, commute and degree share against the county, state and US. UK: council, ward, constituency, rural or urban, national park; England deprivation deciles; England and Wales median sale prices by property type for the postcode sector. |
| `flood_risk` | FEMA flood zone in the US (A and V zones mean lenders usually require flood insurance); Environment Agency Flood Zone 1, 2 or 3 in England. |
| `crime_nearby` | Police-recorded crime within 1 mile for the latest month, by type (England, Wales, Northern Ireland). |
| `who_can_reach` | People living within each drive time (up to 4 bands, 15 minutes to 5 hours). US Census 2020 block groups, WorldPop 2020 for the UK. |
| `drive_times` | Drive minutes and road miles to up to 20 places, or automatically to the nearest town, big cities and airports. |
| `nearby_nature` | Notable lakes, rivers, coast, islands, mountains, national parks, parks, golf, ski, marinas, museums and attractions, with miles, direction and drive minutes. Measures the real distance to the shore or park boundary. |
| `plot_size` | Acres, hectares, square feet and perimeter of a parcel polygon you pass, or of the mapped outline at the address. |
| `map_image` | US aerial photo and topo map PNG links for the site (USGS, public domain), plus Google Maps and OpenStreetMap links. |
| `locate_address` | Address or UK postcode to latitude and longitude, with the source. |
| `list_capabilities` | Coverage, data sources and licences, limits. |

## Connect

**Claude Code**

```bash
claude mcp add --transport http listing-location-toolkit https://listing-location-toolkit.nerolabs.workers.dev/mcp
```

**Claude Desktop / claude.ai:** Settings, Connectors, Add custom connector, paste the URL above.

**Cursor, Windsurf, VS Code and other MCP clients**

```json
{
  "mcpServers": {
    "listing-location-toolkit": {
      "url": "https://listing-location-toolkit.nerolabs.workers.dev/mcp"
    }
  }
}
```

## Example

Call `listing_location_pack` with `{"address": "7090 State Route 80, Cooperstown, NY 13326"}` (a lakeside inn on Otsego Lake). The `listing_lines` that came back, live, 09-11-2026:

```json
[
  "Drive times: Utica 46 min, Albany 1 hr 21 min, Syracuse 1 hr 39 min, New York City 3 hr 43 min and John F. Kennedy International Airport (JFK) 3 hr 57 min.",
  "About 380,000 people live within a 1 hour drive, about 2.5 million within 2 hours and about 30 million within 4 hours (US Census 2020).",
  "Waterfront: on the edge of Otsego Lake (within 170 m of the water).",
  "Parks, nature reserves and protected land: Glimmerglass State Park (1.0 miles, 15 min drive), Betty and Wilbur Davis State Park (9.7 miles, 29 min drive) and Gilbert Lake State Park (18 miles, 48 min drive).",
  "Museums, castles and attractions: Fenimore Art Museum (5.7 miles, 8 min drive), National Baseball Hall of Fame and Museum (6.8 miles, 10 min drive) and Arkell Museum (18 miles, 32 min drive)."
]
```

The full answer also carries each drive time with road miles and raw router minutes, the people count per band with its method, the nearby places by category with direction and distance, map links and a `sources` list. For a lakeside test in England, try `{"address": "LA22 9HA"}` (Lake District).

For a home buyer, call `home_buyer_report` with `{"address": "LA22 9HA"}` (Ambleside, Lake District). Some of the `listing_lines` that came back, live, 09-11-2026:

```json
[
  "Primary and elementary schools nearby: Ambleside CofE Primary School (0.4 miles, about 10 min walk; Ofsted report card (Jun 2026): achievement Expected standard, ...), Grasmere CofE Primary School (2.9 miles, 7 min drive; Ofsted Good (Mar 2020); ungraded check Mar 2025: Standards maintained) and ...",
  "School admissions for this address are run by Westmorland and Furness council (academies, free schools and faith schools may set their own rules).",
  "15 minute walk check: 7 of 7 everyday needs within about a 15 minute walk (a food shop, a primary or elementary school, a doctor, a pharmacy, a park or playground, a bus stop or station and a cafe or pub). Most everyday needs are within a short walk.",
  "The neighbourhood is among the 40% least deprived in England (decile 7 of 10, where 10 is least deprived; English Indices of Deprivation 2025). Crime decile 6, living environment decile 3.",
  "Homes in LA22 9 sold for a median £325,000 over the 12 months to Sep 2026 (17 sales: detached £694,000 (3 sales), semi-detached £402,500 (4 sales), terraced £300,000 (7 sales), flat £325,000 (3 sales); HM Land Registry).",
  "Environment Agency Flood Zone 3 (from rivers): a high chance of flooding, 1% or more a year from rivers or 0.5% from the sea, not counting flood defences.",
  "Police recorded 18 crimes and incidents within 1 mile in Aug 2026 (1 within 400 m); most common: violence and sexual offences 7, criminal damage and arson 3 and drugs 2."
]
```

In the US, `schools_nearby` for the Cooperstown inn names the school district the address is in (Cherry Valley-Springfield Central School District) and the schools that district runs, which is not the same as the nearest school.

## How the numbers are made

- **People within a drive:** residents grouped into sectors by direction and distance, each sector's population centre timed by car, and sectors close to a band edge split finer and timed again. Checked against a full tract-by-tract build: within 1 to 5% at 1 to 4 hours. Bands under 1 hour are rougher. Residents only; people across a national border are not counted.
- **Drive minutes:** the OSRM car router on OpenStreetMap roads, scaled to match Google Maps usual-traffic minutes (checked on 14 US routes: 12 came out 4 to 21% above Google, so on the cautious side, and 2 were 7 to 9% under). The unscaled router minutes are returned too. UK routes are not yet checked against Google. Rush hour can be longer.
- **Nearby places:** notable named places from Wikidata. Distances are to each place's centre point, except `edge_km`, measured to the shore or boundary from its OpenStreetMap outline.
- **Schools and catchments:** there is no national catchment map in the UK or the US. In the US the server reads the official school district boundary for the address and lists the schools that district runs; the district decides which one serves the address. In England it names the council that runs admissions and explains that distance catchments change every year. Ofsted stopped giving overall grades in September 2024 and now publishes report cards; the server shows whichever is latest, with its date.
- **Walk minutes:** straight-line distance at 4.8 km/h with 30% added for the street layout. The 15 minute walk check counts a food shop, primary school, doctor, pharmacy, park or playground, bus stop or station, and a cafe or pub.
- **Plot size:** measured on the ground from the polygon. An OpenStreetMap outline is not a legal boundary, so the server says "about" and asks you to check the deed.

## Sources and licences

| Data | Source | Licence |
|---|---|---|
| US population | US Census Bureau, 2020 Census centers of population by block group | Public domain |
| UK population | WorldPop 2020, 1 km, UN adjusted | CC BY 4.0 |
| Roads and drive times | OpenStreetMap via the OSRM router | ODbL |
| Nearby places | Wikidata | CC0 |
| Shorelines, park boundaries, site outlines | OpenStreetMap via Nominatim | ODbL |
| US addresses | US Census Geocoder | Public domain |
| UK postcodes | postcodes.io (Ordnance Survey and ONS open data) | OGL |
| US aerial and topo images | USGS The National Map | Public domain |
| England schools | Get Information about Schools (DfE) | OGL |
| England school ratings | Ofsted management information, latest inspections | OGL |
| US schools | NCES Common Core of Data 2024-25 and Private School Survey 2023-24 | Public domain |
| School districts, census tracts | US Census Geocoder geographies | Public domain |
| Everyday places, Welsh and Scottish schools | OpenStreetMap | ODbL |
| US neighbourhood figures | American Community Survey 2020-2024 5-year | Public domain |
| England deprivation | English Indices of Deprivation 2025 | OGL |
| England and Wales sale prices | HM Land Registry Price Paid Data | OGL |
| US flood zones | FEMA National Flood Hazard Layer (via Esri Living Atlas) | Public domain |
| England flood zones | Environment Agency Flood Map for Planning | OGL |
| UK street crime | data.police.uk | OGL |

Every answer carries its own `sources` list, so the credit lines can go straight into the listing.

## Limits

Up to 4 drive bands per call, each 15 minutes to 5 hours. Up to 20 destinations (6 by name). Nearby search up to 40 miles. Polygons up to 5,000 points. The people count, the nearby place list and the home buyer tools cover the US and UK; drive times and plot size work anywhere roads are mapped. Ofsted ratings and deprivation cover England; sale prices England and Wales; flood zones the US and England; street crime England, Wales and Northern Ireland. US crime by address is not included: there is no free national source.

## Privacy

Addresses are answered in memory and never stored by this server. To find the pin, the address is sent to the geocoder named in the answer (US Census Geocoder, postcodes.io or Nominatim), and coordinates are sent to the router and Nominatim. To see which tools get used, each call records the tool name, whether it succeeded, the client name your app reports, the country and a one-way hashed caller ID. Your addresses, your arguments and your IP address are never kept in that log.

Built by **Nero Labs**.
