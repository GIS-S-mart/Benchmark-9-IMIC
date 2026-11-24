# IMIC – Input Data

This folder contains all the **input files** required to generate and run the IMIC study scenarios: 
Warehouse description, equipment parameters, scenario configuration, and starting instances.

---

## 📁 Folder structure

```
imic_50_batchIN/
├── config_01/
│   └── 40_AGV/
│       ├── instance_01.json
│       ├── ...
│       └── instance_05.json
├── config_02/
│   └── 40_AGV/
│       ├── instance_01.json
│       ├── ...
│       └── instance_05.json
├── config_03/
│   └── 60_AGV/
│       ├── instance_01.json
│       ├── ...
│       └── instance_05.json
├── config_04/
│   └── 60_AGV/
│       ├── instance_01.json
│       ├── ...
│       └── instance_05.json
├── config_01.yaml
├── config_02.yaml
├── config_03.yaml
├── config_04.yaml
├── geometry.yaml
├── graph.json
└── scenario_IMIC.yaml
```

| File type | Purpose | Level |
|---|---|---|
| `scenario_IMIC.yaml` | General system parameters (layout, elevator, AGV, time horizon) | Shared by all configs |
| `geometry.yaml` | Physical dimensions of the warehouse | Shared by all configs |
| `graph.json` | Directed network graph (nodes, positions, stations) | Shared by all configs |
| `config_XX.yaml` | Generation parameters for one configuration (stock, SKUs, number of AGVs…) | One per configuration |
| `config_XX/<N>_AGV/instance_YY.json` | Generated instances (initial state of AGVs, missions IN/OUT, initial storage) | 5 instances per configuration |

---

## 🧩 File descriptions

### 1. `scenario_IMIC.yaml` – Scenario parameters
Reference file describing the system and its equipment. It is organized in four blocks:
- **`Layout`**: warehouse topology (nb Alley, nb picking/deposite stations, nbTube, nbBay, nbElevatorTrack)
- **`Elevator`**: elevator characteristics (ang/release times on the ground and in the tube)
- **`AGV`**: robot characteristics (dimensions, pick/drop time for stock and for base)
- **`Scenario`**: time horizon (`temporalHorizon`) and IN/OUT base periods

### 2. `geometry.yaml` – Warehouse geometry
Physical dimensions used to build the layout and compute distances:
- **`LayoutDimensions`**: case dimensions, spacings, bay length, alley width, distances between levels / alleys / tracks, etc.
- **`CurvedEdge`**: radius and length of curved arcs
- **`ElevatorDimensions`**: elevator footprint
- **`BasesDimensions`**: base footprint

### 3. `graph.json` – Network graph
**Directed** graph describing the AGV traffic network.
- **`graph.name`**: layout configuration identifier (encodes the warehouse parameters)
- **`nodes`**: list of nodes (type, label, position coordinates)
- **`edges`**: list of nodes couples
  
### 4. `config_XX.yaml` – Configuration of an instance series
One file per configuration driving instance generation:
- **`stockFillingRate`**: Stock filling rate (in %)
- **`skewness`**: SKU distribution coefficient in the stock and total nb of SKUs
- **`maxBatchSizeIN`**: Maximum size of an incoming batch
- **`numberInstances`**: Nb of instances to generate per configuration
- **`numberAGV`**: List of AGV fleet sizes tested

### 5. `config_XX/<N>_AGV/instance_YY.json` – Instances

Each `config_XX/<N>_AGV/` folder contains **5 instances**. The `<N>` prefix (`40` or `60`) corresponds to the AGV fleet size. Content of an instance:

- **`graph_config`**: identifier of the associated graph (see `graph.json`)
- **`name`**: instance name
- **`AGV`**: dictionary of robots
- **`missionsOUT`**: dictionary of missionsOUT (id, pallet_id, sku, date, DS, type, rank)
- **`missionsIN`**: dictionary of missionsIN (id, sku, date, BASE, type)
- **`skuInitialStock`**: list of sku with the initial number of references 
  
## 🔢 Configuration summary

| Configuration | Folder | AGV fleet | Instances |
|---|---|---|---|
| `config_01` | `config_01/40_AGV/` | 40 | 5 |
| `config_02` | `config_02/40_AGV/` | 40 | 5 |
| `config_03` | `config_03/60_AGV/` | 60 | 5 |
| `config_04` | `config_04/60_AGV/` | 60 | 5 |
