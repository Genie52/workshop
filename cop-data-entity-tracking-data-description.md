# Maritime Vessel Tracking Dataset

## What This Dataset Contains
A complete tracking system for 150 ships over 3 months, showing where they go and what happens to them. Think of it like a maritime GPS history combined with incident reports - you can follow individual vessels and see their complete story.

## Quick Start
- **150 ships tracked** continuously over 3 months
- **Position updates** every 6 hours (4 times per day)
- **Incident reports** when something noteworthy happens
- **Ship categories**: Commercial cargo, military vessels, fishing boats, submarines
- **Complete history**: Every ship's movements and events in one dataset

## Dataset Structure - Three Connected Tables

### 1. Ships (Entities)
**What it contains**: Basic information about each vessel
- Ship name, type, and size
- Country flag and home port
- Maximum speed and capabilities
- When first/last seen in the dataset

### 2. Positions
**What it contains**: Where each ship was at specific times
- GPS coordinates every 6 hours
- Speed and direction of travel
- How the position was detected (AIS, radar, satellite)
- Position accuracy estimate

### 3. Events
**What it contains**: Notable incidents involving ships or areas
- **Ship-specific events**: Distress calls, collisions, zone violations
- **Area events**: Storms, navigation hazards, search operations
- Event severity and current status
- Links to specific ships when relevant

## Ship Categories and Types

| Category | Percentage | Examples | Typical Speed |
|----------|------------|----------|---------------|
| **Commercial** | 25% | Cargo ships, tankers, cruise ships | 10-30 knots |
| **Military** | 21% | Destroyers, frigates, patrol boats | 15-35 knots |
| **Fishing** | 31% | Trawlers, fishing vessels | 8-20 knots |
| **Submarines** | 24% | Attack subs, research subs | 15-25 knots |

## Example: Following a Ship's Journey

### Sample Cargo Ship "Atlantic Trader"
```
Day 1: Created in dataset near New York
├── Position 1: 40.7°N, 74.0°W (New York Harbor)
├── Position 2: 40.8°N, 73.5°W (heading east, 18 knots)
├── Position 3: 41.0°N, 72.8°W (continuing east)
└── Position 4: 41.2°N, 72.0°W (steady course)

Day 2: Event occurs
├── Position 5: 41.5°N, 71.0°W (normal transit)
├── EVENT: Equipment failure (engine trouble)
├── Position 6: 41.5°N, 71.0°W (stopped for repairs)
└── Position 7: 41.6°N, 70.5°W (resumed journey, slower speed)

Day 3: Continues journey
├── Position 8: 42.0°N, 69.8°W (back to normal speed)
└── ... continues until reaching destination or leaving area
```

## Types of Events

### Ship-Specific Events (70% of events)
Events that happen to individual vessels:

| Event Type | What Happened | Example |
|------------|---------------|---------|
| **Distress Signal** | Ship in emergency | Engine failure, medical emergency |
| **Zone Violation** | Entered restricted area | Military zone, protected waters |
| **Collision** | Hit another vessel | Two ships collided |
| **Equipment Failure** | Mechanical problems | Radar down, engine trouble |
| **Suspicious Activity** | Unusual behavior | Unexpected route change |

### Area Events (30% of events)
Events affecting geographic regions:

| Event Type | What Happened | Example |
|------------|---------------|---------|
| **Storm Warning** | Severe weather | Hurricane, high winds |
| **Navigation Hazard** | Obstacle in water | Debris, iceberg |
| **Search & Rescue** | Missing person/vessel | Coast Guard operation |
| **Military Exercise** | Naval training | Area temporarily closed |
| **Oil Spill** | Environmental incident | Tanker leak, cleanup operation |

## How Ship Tracking Works

### Position Updates
- **Frequency**: Every 6 hours (4 times per day)
- **Total Positions**: 53,672 position records over 3 months
- **Movement**: Ships move realistically based on speed and direction
- **Course Changes**: 10% chance of changing direction at each update

### Data Sources
- **AIS (Automatic Identification System)**: Most accurate, ±5-10 meters
- **Radar**: Medium accuracy, ±20-30 meters  
- **Satellite**: Variable accuracy, ±10-50 meters

### Ship Lifecycle
- **Active**: Ship regularly reports positions (most ships)
- **Inactive**: Ship left the monitoring area (2% leave daily)
- **Lost**: Ship missing for extended period (rare)

## What You Can Do With This Data

### Track Individual Ships
- **Complete History**: See everywhere a ship has been
- **Behavior Analysis**: Identify normal vs. unusual patterns
- **Route Planning**: Understand common shipping routes
- **Incident Investigation**: What happened before/after events

### Monitor Areas
- **Traffic Density**: How many ships in specific regions
- **Environmental Impact**: Ships affected by weather events
- **Security Monitoring**: Unusual activity in sensitive areas
- **Search Operations**: Ships available for rescue assistance

### Analyze Patterns
- **Shipping Routes**: Most common paths between ports
- **Seasonal Changes**: How traffic varies by time of year
- **Event Correlation**: Do certain events happen together?
- **Risk Assessment**: Which areas have most incidents

## Common Queries You Can Run

### Ship-Focused Questions
- "Show me all positions for ship X over the last month"
- "Which ships were near the collision site?"
- "What's the movement history of suspicious vessel Y?"
- "Find all fishing vessels that entered restricted zones"

### Area-Focused Questions  
- "What events happened in this geographic region?"
- "Which ships are currently in the storm warning area?"
- "Show me all incidents within 50km of this port"
- "What's the ship traffic density in this shipping lane?"

### Time-Based Questions
- "What happened during the storm on March 15th?"
- "Show me ship movements during the military exercise"
- "Which vessels were active during the search operation?"
- "Track how the oil spill affected nearby ships"

## Data Quality and Limitations

### What's Reliable
- **Position Accuracy**: Within 5-50 meters depending on source
- **Time Stamps**: Accurate to the minute
- **Ship Identity**: Each vessel has unique, persistent ID
- **Event Linkage**: Events correctly linked to involved ships

### What to Watch For
- **Missing Positions**: Some ships may have gaps in tracking
- **Course Changes**: Sudden direction changes are simulated, may not reflect real navigation
- **Event Timing**: Events are randomly distributed, not based on real incidents
- **Submarine Tracking**: Limited position updates (realistic for security)

## Getting Started

### Essential Files
1. **entities.json**: List of all 150 ships with basic information
2. **positions.json**: All position updates (53,672 records)
3. **events.json**: All incidents and notable occurrences

### Typical Analysis Workflow
1. **Load Ship Data**: Import the three main data files
2. **Pick a Ship**: Choose a vessel to follow
3. **Plot Movement**: Map the ship's positions over time
4. **Find Events**: Look for incidents involving that ship
5. **Analyze Patterns**: Compare with other similar vessels

### Sample Analysis Ideas
- **Route Optimization**: Find the most efficient paths between ports
- **Safety Analysis**: Identify high-risk areas with frequent incidents
- **Traffic Management**: Understand congestion patterns
- **Emergency Response**: Analyze how quickly help arrives during distress calls

---

## Technical Details (Advanced Users)

## Technical Details (Advanced Users)

### Data Structure Overview
```
Root Dataset
├── metadata (dataset info)
├── entities (150 ships)
├── positions (53,672 location records)  
└── events (incident reports)
```

### Key Relationships
- **One ship** → **Many positions** (tracking over time)
- **One ship** → **Many events** (incidents involving that ship)
- **One event** → **One or zero ships** (some events are area-based)

### File Sizes and Performance
- **entities.json**: ~50KB (ship information)
- **positions.json**: ~15MB (all position updates)
- **events.json**: ~2MB (all incidents)
- **Total Dataset**: ~17MB uncompressed

## Glossary

**AIS**: Automatic Identification System - GPS-based tracking system used by ships
**Entity**: A persistent object (ship) that exists over time
**Event**: An incident or notable occurrence at a specific time and place
**MMSI**: Maritime Mobile Service Identity - unique 9-digit ship identifier
**Position Update**: A single GPS location report from a ship
**Track**: The complete path of a ship's movement over time
**Zone Violation**: When a ship enters a restricted or prohibited area

## Comparison: Entity-Tracking vs. Event-Only Data

| Aspect | Entity-Tracking (This Dataset) | Event-Only Data |
|--------|-------------------------------|-----------------|
| **Ship Identity** | Persistent - same ship tracked over time | Temporary - each event is independent |
| **Movement History** | Complete path available | Only event locations |
| **Behavior Analysis** | Can analyze patterns over time | Limited to single incidents |
| **Data Size** | Larger (continuous tracking) | Smaller (events only) |
| **Use Cases** | Route analysis, behavior patterns | Incident response, alerts |

This entity-tracking approach gives you the complete story of each vessel, making it ideal for understanding maritime operations, analyzing shipping patterns, and investigating incidents with full context.


