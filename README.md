# ESCALATE Fleet Operation Optimization Data

This repository contains optimization data generated as part of the EU ESCALATE project deliverable D5.4, demonstrating fleet operation optimization for zero emission vehicles.

## Overview

The ESCALATE project developed an advanced fleet operation optimization tool that enables fleet operators to efficiently integrate zero emission vehicles into their operations. This tool uses innovative AI methodologies combined with high-detail simulation models to optimize the fleet operation for all vehicles (routing, charging strategy and hydrogen refueling strategy) while considering energetic constraints, charging requirements, and hydrogen refueling needs.

## Repository Contents

This repository contains input data and optimization results for two fictitious long haul fleet scenarios:

### Input Data
- **`jobs.json`** - Customer delivery orders with pickup/delivery locations, time windows, and cargo specifications
- **`locations.json`** - Infrastructure data including depot, charging stations, and hydrogen refueling stations
- **`vehicles_ICEV_fleet.json`** - Fleet composition for ICEV-only scenario (5 conventional diesel trucks)
- **`vehicles_mixed_fleet.json`** - Fleet composition for mixed scenario (1 ICEV, 2 Pilot 4 BEV, 2 Pilot 2 FCEV)

### Output Data
- **`optimized_ICEV_fleet_operation/solution.json`** - Optimized tours and operations for conventional fleet
- **`optimized_mixed_fleet_operation/solution.json`** - Optimized tours and operations for mixed zero-emission fleet

The fleet operation optimization model was given the same locations and jobs for two optimizations. One optimization was conducted for 5 long haul ICEV and one optimization was conducted where 4 vehicles were swapped with 2 Pilot 4 and 2 Pilot 2 of the project. In the mixed fleet scenario, a charging station and a hydrogen refueling station is placed at the depot. The optimization model optimizes the vehicles based on the given vehicles and also the tour for each vehicle. The model aims for the most efficient total cost of operation while fulfilling all jobs.

## Data Structure

### Jobs
Each job contains:
- Unique job ID
- Package mass and volume
- Service time requirements
- Origin and destination locations with time windows

### Locations
Infrastructure points including:
- **Depot**: Vehicle starting/ending location (Ulm, Germany)
- **Charging Stations**: High-power charging locations across Europe (400kW capacity)
- **Hydrogen Refueling Stations**: H2 refueling infrastructure

### Vehicles
Vehicle specifications include:
- **ICEV 40t**: Conventional diesel trucks
- **ESCALATE Pilot 4**: Battery electric vehicles (1,100 kWh capacity, 400kW charging)
- **ESCALATE Pilot 2**: Fuel cell electric vehicles (68kg H2 capacity, 30.5 kWh buffer battery)

### Solution Data
Optimization results contain:
- **Summary**: Total cost breakdown (TCO CAPEX, energy, wages, tolls, CO2, etc.)
- **Tours**: Detailed vehicle tours with:
  - Stop sequences and timing
  - Load management
  - Energy state tracking (fuel/battery/hydrogen)
  - Charging/refueling stops
  - Detailed time tracking:
    - **`step_resting_number`** - Number of en route rests between the stops at any rest area next to the road
    - **`step_resting_time`** - Total duration of en route rests between the stops at any rest area next to the road
    - **`step_nighting_number`** - Number of en route overnight rests between the stops at any rest area next to the road
    - **`step_nighting_time`** - Total duration of en route overnight rests between the stops at any rest area next to the road
    - **`delta_driving_time`** - Driving time between the stops
    - **`delta_waiting_time`** - Time the driver waits after arriving at the stop and being serviced
    - **`delta_serving_time`** - Time of being servied (loaded/unloaded) on site
    - **`delta_charging_time`** - Duration of the charging process on site
    - **`delta_hydrogen_refueling_time`** - Duration of the hydrogen refueilng process on site
    - **`delta_resting_time`** - Additional rest time of the driver on site
    

The model calculates the Total Cost of Ownership (TCO) for the time horizon of the optimization.

### Visualization
Visualtzation files are added for a better understanding of the data.
- **`fleet_operation_map.html`** - Top-down view of optimized tours of all vehicles on a map. For a clearer overview, the vehicle tours are not only visualized with the roads actually driven, but also with straight connected lines between the stops. The purpe dashed lines indicate the pickup and delivery locations of the jobs.
- **`vehicle_charts.html`** - Plots of energy (fuel, electric SoC, hydrogen SoC) and payloads (mass, volume) for all used vehicles along their trip. The vertical line at the end of eSoC and hSoC plots indicate charging and refueling at the depot, which can be done slow or fast before the next use of the vehicle. Since this duration is unknown, it's simplified and visualized as instant charged/refueled.

## Technical Implementation

The optimization tool integrates:
- **Route Planning**: Efficient sequencing of customer visits
- **Energy Management**: Accurate prediction of energy consumption and state of charge
- **Infrastructure Utilization**: Strategic placement of charging/refueling stops
- **Regulatory Compliance**: Driver working time and rest period requirements
- **Cost Optimization**: Total Cost of Ownership (TCO) minimization

## Usage

The usage of 

This data demonstrates the practical implementation of zero emission vehicle integration in freight operations, showing:
1. Feasibility of mixed fleet operations with current technology
2. Trade-offs between operational costs and environmental benefits
3. Infrastructure requirements for zero emission freight transport
4. Optimization strategies for energy management and route planning

## Project Context

This work was conducted as part of the EU ESCALATE project, which developed innovative zero emission commercial vehicles and supporting technologies. The optimization tool enables fleet operators to transition to sustainable transport solutions while maintaining operational efficiency.

## Data Format

All data files use JSON format with UTF-8 encoding. Coordinates are provided in WGS84 decimal degrees. Times use ISO 8601 format (UTC). Distances are in meters, masses in kg, and energy values in Ws.

## Reference

The Total Cost of Ownership (TCO) parameters in this optimization model are based on:

**Basma, H., & Rodríguez, F. (2023). A total cost of ownership comparison of truck decarbonization pathways in Europe. International Council on Clean Transportation. Working Paper 2023-28.**

## License

This data is provided as part of the ESCALATE project deliverable and is intended for research and demonstration purposes.

## Author

Theo Koch  
Intitute for Automotive Engineering Aachen (ika)  
RWTH Aachen University  
theo.koch@ika.rwth-aachen.de 
