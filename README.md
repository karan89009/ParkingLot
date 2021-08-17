# ParkingLot

There exists a parking lot that contains multiple floors. Multiple entries and exits points. The parking lot operates on a first come first served basis. Entry is recorded at the entry point and payment is done at the time of exit.

Each floor can hold upto ‘n’ vehicles at any given point in time. The floor contains multiple parking slots for different types of vehicles.
1. Cars
2. Motorbikes
3. Large vehicles.

Created an automated ticketing system that allows customers to use the parking lot without human intervention. A ticket shall be issued to a vehicle when enters the parking lot.
The number of slots available in the parking lot is segmented in 6:3:1 fashion, which means, a parking floor can hold 6 cars, 3 motorbikes and 1 large vehicle. This can be configurable for each floor.

The vehicle contains:
1. Registration number of the vehicle.
2. Color of the vehicle.
3. Type of the vehicle.

The vehicle is allotted a parking slot which is nearest to the entry. On the vehicle’s exit, the slot that was previously occupied, is marked as available.

The system handles, the following use cases.

## Create a parking lot with ‘x’ floors and 'n' capacity

## Create a floor with a given vehicle parking configuration ratio

**API:** http://localhost:5000/parking

**Type:** POST

**Payload:** 

        {
          "floor":3,
          "capacity":10
        }
        
_**Note:** The capacity should be multiple of 10 in order to divide it into 6:3:1 ratios_

**Output:**

        {
            "buffer": [
                6,
                3,
                1
            ],
            "_id": "611c2c15002682181c3c70b4",
            "floor": 3,
            "capacity": 10
        }

_**Note:** buffer: is ratio buffer where 1st element is car capacity per floor, 2nd element is bike capacity per floor and 3rd element is large_vehicle capacity per floor._

## Park a vehicle.

**API:** http://localhost:5000/vehicle/booking

**Type:** POST

**Payload:**

      {

          "registrationNumber":"UP53AC9548",

          "color":"cherry",

          "type":"bike"

   }
   
_**Note:** Type can be only "bike","car","large_vehicle"_
_RegistrationNumber can be alphanumeric only_
        
        
**Output:**

        {
            "slot_number": "1F:1",
            "_id": "611c2da8002682181c3c70f3",
            "registrationNumber": "UP53AC9548",
            "color": "cherry",
            "type": "car",
        }
        
**_Note:_** _slot_number: 1F:1 means 1st counter which is at 1st floor.
            If same registration number car is booked it will throw error : "Already in Parking!!!"_
            
            
## Exit a vehicle

 **API:** http://localhost:5000/vehicle/exit/<RegistrationNumber>
        
        eg: http://localhost:5000/vehicle/exit/UP53AC9548
        
**Type:** POST
        
**Output:**
        
                  {
                    "fare": 30
                  }
        
        
_**Note:**_ _fare is calculate using formula:
                fare= no_of_hours_car_in_parking*vehicle_type_charge_
                _If vehicle less than an hour the complete 1 hour charge is applied_
        
        
                Vehicle_type          charges/hour
                1. car                   30
                2. bike                  10
                3. large_vehicle         50
  
## Get the parking status of the entire parking lot
        
**API:** http://localhost:5000/parkingStatus
        
**Type:** GET

**Output:**
        
        
                {
                    "available": 59,
                    "unavailable": 1
                }
        
        
## Get the parking status of the given parking floor
        
**API:** http://localhost:5000/parkingStatus/<floor_number>
        eg: http://localhost:5000/parkingStatus/1
        
**Type:** GET

**Output:**
        
        
                {
                    "available": 19,
                    "unavailable": 1
                }
       

## Registration numbers of all cars of a particular colour.
9. Slot number in which a car with a given registration number is parked.
9. Slot numbers of all slots where a car of a particular colour is parked
