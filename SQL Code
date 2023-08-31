use superstore;
show tables;
select * from flight;

-- No_of_passengers by Type_of_travel, class, gender, flight_distance and customer_type

select Type_of_travel, class, customer_type, gender, flight_distance, count(id) as No_of_passengers
from flight
group by 1,2,3,4,5;


-- Number ofpassengers by gender
-- using CUME_DIST we get that No_of_passengers from both genders are equal

select gender, count(id) as No_of_passengers,
cume_dist () over(order by count(id))
from flight
group by gender;


-- segregate age with <=27 , Millennials and >=42 and find out which category has highest number of travelers.

select Type_of_travel, class, count(id) as total_passengers,
CASE
	when age <= 27 then "Gen_Z or below"
    when age >= 42 then "Gen_X and above"
    else "Millennials"
end as age_category
 from flight
 group by  1,2, age_category 
 order by total_passengers desc;


-- Flight_distance categorised by distance_category along with type_of_travel and class

select type_of_travel, count(id),0 as total_passengers,
CASE
	when flight_distance <= 2500 then "domestic"
    else "international"
end as Distance_category
 from flight
 group by type_of_travel, distance_category
 order by distance_category;
 
 
 -- PASSENGERS CATEGORIZED AS PER LOYALTY PROGRAM AND SEAT CLASS
 
 select type_of_travel, class, count(id) as total_passengers 
 from flight
 where customer_type = "loyal customer"
 group by 1,2;
 
 
-- Find out Target Passenger as per specified conditions
 
 select type_of_travel, class, count(id) as total_passengers, 
 CASE
	when Customer_type = "Loyal customer" and flight_distance <= 2500 and class in("Business", "Eco") then "Target passenger"
    else "New or unenrolled"
end as Cutomer_category
 from flight
 group by type_of_travel, class, customer_type, flight_distance;
 
 
 -- all passenger ratings

select Class as 'Seat_Class' , Type_of_Travel as 'Purpose_of_travel', customer_type, count(id) No_of_passengers,
avg(flight_distance),
avg(ease_online_booking),
avg(Food_drink),
avg(Online_boarding),
avg(Seat_comfort),
avg(inflight_entertainment),
avg(onboard_service),
avg(legroom_service),
avg(baggage_handling),
avg(checkin_service),
avg(inflight_service),
avg(cleanliness)
from flight 
group by class, type_of_travel, customer_type
order by type_of_travel, customer_type;


 -- Ratings by Target passengers

select Type_of_Travel as 'Purpose_of_travel', Class as 'Seat_Class', count(id) No_of_passengers,
avg(ease_online_booking) ,
avg(Food_drink) ,
avg(Online_boarding) ,
avg(Seat_comfort) ,
avg(inflight_entertainment) ,
avg(onboard_service) ,
avg(legroom_service) ,
avg(baggage_handling) ,
avg(checkin_service) ,
avg(inflight_service),
avg(cleanliness)
from flight 
where Customer_type = "Loyal customer" and flight_distance <= 2500 and class in("Business", "Eco")
group by type_of_travel, class
order by No_of_passengers;
