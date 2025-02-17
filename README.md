# WAVY---CITY-BUS-TRANSIT-DASHBOARD

https://app.powerbi.com/groups/me/reports/69eeb5fd-ab64-4242-a4be-511b46f7d7a5/ade936fd92b394813059?experience=power-bi

## Features Implemented

### 1. Impact of Trip Direction on Delays
**Formula:**
```plaintext
Impact_Trip_Direction = SUM(ITMS[trip_delay])
```
**Description:** Aggregates the total trip delay for each trip direction, helping identify which directions experience more significant delays.

---

### 2. Total Trip Delay by Vehicle and Start Time
**Formula:**
```plaintext
Total_Trip_Delay_Vehicle = SUM(ITMS[trip_delay])
```
**Description:** Tracks total trip delay for each vehicle, with start time on the x-axis and delay on the y-axis.

---

### 3. Traffic Flow and Stop Density Across Locations
**Formula:**
```plaintext
Traffic_Flow_Stop_Density = SUM(ITMS[speed])
```
**Description:** Compares traffic flow and stop density to identify high-congestion areas.

---

### 4. Total Speed by Route
**Formula:**
```plaintext
Total_Speed_Route = SUM(ITMS[speed])
```
**Description:** Aggregates total speed by each route to assess speed performance.

---

### 5. Total Speed by Observation Date Time
**Formula:**
```plaintext
Total_Speed_ObservationDateTime = SUM(ITMS[speed])
```
**Description:** Tracks speed trends over time based on observation timestamps.

---

### 6. Fleet Utilization
**Formula:**
```plaintext
FleetUtilization = COUNT(ITMS[trip_id]) / DISTINCTCOUNT(ITMS[vehicle_label])
```
**Description:** Calculates how much of the fleet is actively used by dividing total trips by unique vehicles.

---

### 7. Count of Route ID by Trip Delay
**Formula:**
```plaintext
Count_Route_TripDelay = COUNT(ITMS[route_id])
```
**Description:** Identifies routes experiencing frequent delays.

---

### 8. Average Speed
**Formula:**
```plaintext
AvgSpeed = AVERAGE(ITMS[speed])
```
**Description:** Computes the average speed of all trips.

---

### 9. Average Delay
**Formula:**
```plaintext
AvgDelay = AVERAGE(ITMS[trip_delay])
```
**Description:** Determines the average trip delay.

---

### 10. Bus Bunching
**Formula:**
```plaintext
BusInterval = DATEDIFF(
    CALCULATE(MAX(ITMS[last_stop_arrival_time])),
    CALCULATE(MIN(ITMS[last_stop_arrival_time]), ALLEXCEPT(ITMS, ITMS[route_id])),
    SECOND
)
```
**Description:** Measures time differences between buses on the same route to detect bunching.

---

### 11. Trips Per Hour
**Formula:**
```plaintext
TripsPerHour = COUNTROWS(ITMS)
```
**Description:** Counts the number of trips per hour.

---

### 12. Geospatial Distribution of Routes and Trip Delays
**Formula:**
```plaintext
Latitude = AVERAGE(ITMS[shape_pt_lat])
Longitude = AVERAGE(ITMS[shape_pt_lon])
```
**Description:** Uses a heatmap to show trip delays across geographic locations.

---

### 13. Route Reliability Index
**Formula:**
```plaintext
Route_Reliability_Index = AVERAGEX(FILTER(ITMS, ITMS[trip_delay] > 0), ITMS[trip_delay])
```
**Description:** Assesses route consistency based on trip delays.

---

### 14. Fleet Efficiency Monitor
**Formula:**
```plaintext
Fleet_Efficiency = DIVIDE(SUM(ITMS[speed]), SUM(ITMS[trip_delay]), 0)
```
**Description:** Evaluates fleet performance by comparing speed and delay.

---

### 15. Maximum Trip Delay
**Formula:**
```plaintext
Max_Trip_Delay = MAX(ITMS[trip_delay])
```
**Description:** Identifies the longest trip delay.

---

### 16. Estimated Arrival Time
**Formula:**
```plaintext
Estimated_TA = 
    VAR Distance = SUM(ITMS[speed]) * (SUM(ITMS[trip_delay]) / 60)
    VAR Time_to_Complete = Distance / AVERAGE(ITMS[speed])
    VAR Current_Time = NOW()
    RETURN Current_Time + Time_to_Complete / 24
```
**Description:** Estimates the vehicle's arrival time based on speed and delays.

---

### 17. CO2 Emissions
**Formula:**
```plaintext
CO2_Emissions_upd = 
    VAR Total_Trip_Delay_Hours = SUM(ITMS[trip_delay]) / 60
    VAR Total_Distance_Traveled = SUM(ITMS[speed]) * Total_Trip_Delay_Hours
    VAR Fuel_Consumption = Total_Distance_Traveled / 10
    VAR CO2_Emission_Factor = 2.31
    RETURN Fuel_Consumption * CO2_Emission_Factor
```
**Description:** Calculates CO2 emissions from trip delays and fuel consumption.

---

### 18. Fuel Efficiency
**Formula:**
```plaintext
Fuel_Efficiency = DIVIDE(SUM(ITMS[speed]), SUM(ITMS[trip_delay]), 0)
```
**Description:** Measures fuel efficiency based on speed and delay data.

