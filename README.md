# WAVY---CITY-BUS-TRANSIT-DASHBOARD

https://app.powerbi.com/groups/me/reports/69eeb5fd-ab64-4242-a4be-511b46f7d7a5/f3f7ea01053d7ddd8c98?experience=power-bi

# Demo

https://drive.google.com/file/d/1OhK83XNl98iA6_c1HTEkP2qIMPWalhCI/view?usp=sharing

## Features Implemented

### 1) Impact of Trip Direction on Delays: 

- **X-axis:** sum of trip_delay 
- **Y-axis:** trip_direction 

**Formula:**  
```plaintext
Impact_Trip_Direction = SUM(ITMS[trip_delay])
```

**Description:**  
This visual shows the impact of different trip directions on delays. It aggregates the total trip delay for each direction, helping identify which directions experience more significant delays.

---

### 1.1) Total Trip Delay by Vehicle and Start Time

- **X-axis:** last_stop_arrival_time  
- **Y-axis:** sum of trip_delay  

**Formula:**  
```plaintext
Total_Trip_Delay_Vehicle = SUM(ITMS[trip_delay])
```

**Description:**  
This chart shows the total trip delay for each vehicle, with the x-axis representing the vehicle label and the y-axis showing the actual trip start time. It helps track how delays vary for each vehicle over time.

---

### 2) Total Trip Delay by Vehicle and Start Time

- **X-axis:** vehicle_label  
- **Y-axis:** actual_trip_start_time  

**Formula:**  
```plaintext
Total_Trip_Delay_Vehicle = SUM(ITMS[trip_delay])
```

**Description:**  
This chart shows the total trip delay for each vehicle, with the x-axis representing the vehicle label and the y-axis showing the actual trip start time. It helps track how delays vary for each vehicle over time.

---

### 3) Traffic Flow and Stop Density Across Locations

- **X-axis:** sum of speed  
- **Y-axis:** sum of last_stop_id  

**Formula:**  
```plaintext
Traffic_Flow_Stop_Density = SUM(ITMS[speed])
```

**Description:**  
This visual compares the traffic flow (sum of speed) and the density of stops (count of last stop IDs) across different locations, helping identify areas with high traffic and stop density.

---

### 4) Total Speed by Route

- **X-axis:** sum of speed  
- **Y-axis:** route_id  

**Formula:**  
```plaintext
Total_Speed_Route = SUM(ITMS[speed])
```

**Description:**  
This visual aggregates the total speed by each route, helping assess the overall speed across different routes.

---

### 5) Total Speed by Observation Date Time

- **X-axis:** observationDateTime  
- **Y-axis:** sum of speed  

**Formula:**  
```plaintext
Total_Speed_ObservationDateTime = SUM(ITMS[speed])
```

**Description:**  
This visual tracks the total speed across different observation date times, helping identify trends and patterns in speed over time.

---

### 6) Fleet Utilisation

**Formula:**  
```plaintext
FleetUtilization = COUNT(ITMS[trip_id]) / DISTINCTCOUNT(ITMS[vehicle_label])
```

**Description:**  
This metric calculates the fleet utilization by dividing the total number of trips by the number of distinct vehicles, giving insights into how much of the fleet is actively used.

---

### 7) Count of Route ID by Trip Delay

- **X-axis:** count of route_id  
- **Y-axis:** trip_delay  

**Formula:**  
```plaintext
Count_Route_TripDelay = COUNT(ITMS[route_id])
```

**Description:**  
This visual shows the count of routes experiencing delays, helping identify routes that are frequently delayed.

---

### 8) Avg Speed

**Formula:**  
```plaintext
AvgSpeed = AVERAGE(ITMS[speed])
```

**Description:**  
This formula calculates the average speed of all trips in the dataset, helping to understand the overall speed performance.

---

### 9) Avg Delay

**Formula:**  
```plaintext
AvgDelay = AVERAGE(ITMS[trip_delay])
```

**Description:**  
This formula calculates the average trip delay across all trips, providing an overview of the typical delay encountered.

---

### 10) Bus Bunching

- **X-axis:** route_id  
- **Y-axis:** BusInterval  

**Formula:**  
```plaintext
BusInterval = DATEDIFF(
    CALCULATE(MAX(ITMS[last_stop_arrival_time])),
    CALCULATE(MIN(ITMS[last_stop_arrival_time]), ALLEXCEPT(ITMS, ITMS[route_id])),
    SECOND
)
```

**Description:**  
This formula calculates the time difference (interval) between the first and last buses of the same route at each stop, helping to identify bus bunching.

---

## Sustainability Insights

### 16) CO2 Emissions

- **Pie Chart**  
- **Legend:** vehicle_label  
- **Values:** CO2_Emissions_upd  

**Formula:**  
```plaintext
CO2_Emissions_upd = 
    VAR Total_Trip_Delay_Hours = SUM(ITMS[trip_delay]) / 60
    VAR Total_Distance_Traveled = SUM(ITMS[speed]) * Total_Trip_Delay_Hours
    VAR Fuel_Consumption = Total_Distance_Traveled / 10
    VAR CO2_Emission_Factor = 2.31
    RETURN Fuel_Consumption * CO2_Emission_Factor
```

**Description:**  
This formula calculates CO2 emissions based on trip delays and vehicle speed, showing the environmental impact of delays.

---

### 17) Fuel Efficiency

- **Columns:** vehicle_label, route_id, fuel_efficiency  

**Formula:**  
```plaintext
Fuel_Efficiency = DIVIDE(SUM(ITMS[speed]), SUM(ITMS[trip_delay]), 0)
```

**Description:**  
Calculates vehicle fuel efficiency by comparing speed and trip delay.


