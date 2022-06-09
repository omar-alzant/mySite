---
title: "Sql -Fifeties- "
date: 2022-06-08
draft: false
project_tags: ["sql"]
status: "sql"
weight: 6
summary: "Write SQL queries to solve a mystery.

"
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://cs50.harvard.edu/x/2022/psets/7/fiftyville/"
        weight: 1
    another_link:
        text: "Another github link"
        icon: "fab alt brands fa-github"
        href: "https://github.com/omar-alzant"
        weight: 2
---


</br>

<strong>
    All the files is included in the github page
    <a href="https://github.com/omar-alzant/files-for-SQLite3"> Here. </a>
</strong>

</br>
</br>

<a href="https://www.w3schools.com/sql/sql_ref_keywords.asp"> To learn SQL </a>
 and   <a href="https://www.sqlstyle.guide/"> This </a>.

</br>
</br>

## A Mystery in Fiftyville :

The CS50 Duck has been stolen! The town of Fiftyville has called upon you to solve the mystery of the stolen duck. Authorities believe that the thief stole the duck and then, shortly afterwards, took a flight out of town with the help of an accomplice. Your goal is to identify:

1- Who the thief is.

2- What city the thief escaped to,and.

3- Who the thief’s accomplice is who helped them escape.


All you know is that the theft took place on July 28, 2021 and that it took place on Humphrey Street.

How will you go about solving this mystery? The Fiftyville authorities have taken some of the town’s records from around the time of the theft and prepared a SQLite database for you, `fiftyville.db`, which contains tables of data from around the town. You can query that table using SQL `SELECT` queries to access the data of interest to you. Using just the information in the database, your task is to solve the mystery.

***

{{<youtube x7Q8tJMi7cQ>}}

***

</br>
</br>

Code -step-by-step- :

```sql
-- Keep a log of any SQL queries you execute as you solve the mystery.
-- Theft of the CS50 duck took place at 10:15am at the Chamberlin Street courthouse

--Interviews were conducted today with three witnesses who were present at the time — each
--of their interview transcripts mentions the courthouse.

--select flight_id, passport_number,seat
--from passengers join flights on flight.id = passengers.flight_id
--where passport_number like '%5773159633%' or  passport_number like '%8496433585%' or passport_number like '%359275073%'


-- the first step , Find out some clues about the crime:

--1
--SELECT description
--FROM crime_scene_reports
--WHERE day = 28 and month = 7 and year = 2020 and street like '%Chamberlin Street%'
-- result:
--Theft of the CS50 duck took place at 10:15am at the Chamberlin Street courthouse. Interviews were conducted
--today with three witnesses who were present at the time — each of their interview transcripts mentions the courthouse.

-- form 1 , we know the time of crime and we move to interviews :

--2
--SELECT  transcript, day ,month, year
--FROM interviews
--WHERE day = 28 and month = 7 and year = 2020
-- result : the interviews;

-- 1- I am working in court, and I saw the person hitting and running away on my way to work this morning.
-- 2-I saw him talking on the phone outside the courtroom at 3:00 pm.
-- 3- At some point within ten minutes of the robbery, I saw the thief get into a car in the court parking lot and drive away.  If she has
-- If you have security footage of the court parking lot, you may want to look up cars that have left the parking lot in that time frame.
-- 4- I don't know the thief's name, but he was someone I recognized.  Earlier this morning, before I got to court, I was
-- I walked by an ATM on Vivre Street and saw the thief withdraw some cash
-- 5- When the thief was leaving the courtroom, they called those with whom he spoke for less than a minute.  On the call, I heard the thief j
-- Saying they were planning to take the first flight out of Fiftyville tomorrow.  Then the thief asked the person on the other end of the phone to buy the airline ticket.

--3
-- after we read the interviews , we can searching the theif
--SELECT *
--FROM courthouse_security_logs
--where day = 28 and month = 7 and year =2020 and activity like '%exit%'

-- result :we chose the ids  between 10:15 and 10:25
--id | year | month | day | hour | minute | activity | license_plate
--260 | 2020 | 7 | 28 | 10 | 16 | exit | 5P2BI95
--261 | 2020 | 7 | 28 | 10 | 18 | exit | 94KL13X
--262 | 2020 | 7 | 28 | 10 | 18 | exit | 6P58WS2
--263 | 2020 | 7 | 28 | 10 | 19 | exit | 4328GD8
--264 | 2020 | 7 | 28 | 10 | 20 | exit | G412CB7
--265 | 2020 | 7 | 28 | 10 | 21 | exit | L93JTIZ
--266 | 2020 | 7 | 28 | 10 | 23 | exit | 322W7JE
--267 | 2020 | 7 | 28 | 10 | 23 | exit | 0NTHK55

--4
--SELECT caller,receiver,duration
--FROM phone_calls
--WHERE day =28 and month =7  and year = 2020 and  duration <60

--result:
--caller | receiver | duration
--(130) 555-0289 | (996) 555-8899 | 51
--(499) 555-9472 | (892) 555-8872 | 36
--(367) 555-5533 | (375) 555-8161 | 45
--(499) 555-9472 | (717) 555-1342 | 50
--(286) 555-6063 | (676) 555-6554 | 43
--(770) 555-1861 | (725) 555-3243 | 49
--(031) 555-6622 | (910) 555-3251 | 38
--(826) 555-1652 | (066) 555-9701 | 55
--(338) 555-6650 | (704) 555-2131 | 54


--5
--SELECT *
--FROM atm_transactions
--WHERE day =28 and month =7 and year = 2020 and transaction_type like '%withdraw%' and atm_location like '%Fifer Street%'

-- result :
--id | account_number | year | month | day | atm_location | transaction_type | amount
--246 | 28500762 | 2020 | 7 | 28 | Fifer Street | withdraw | 48
--264 | 28296815 | 2020 | 7 | 28 | Fifer Street | withdraw | 20
--266 | 76054385 | 2020 | 7 | 28 | Fifer Street | withdraw | 60
--267 | 49610011 | 2020 | 7 | 28 | Fifer Street | withdraw | 50
--269 | 16153065 | 2020 | 7 | 28 | Fifer Street | withdraw | 80
--288 | 25506511 | 2020 | 7 | 28 | Fifer Street | withdraw | 20
--313 | 81061156 | 2020 | 7 | 28 | Fifer Street | withdraw | 30
--336 | 26013199 | 2020 | 7 | 28 | Fifer Street | withdraw | 35

--6
--SELECT *
--FROM people

-- we search with the result for the same license plate who. are resulted before,:

--license_plate | hour | minute | name | phone_number | passport_number | license_plate
--5P2BI95 | 10 | 16 | patrick | (725) 555-4692 | 2963008352 | 5P2BI95
--94KL13X | 10 | 18 | Ernest | (367) 555-5533 | 5773159633 | 94KL13X. ***************
--6P58WS2 | 10 | 18 | Amber | (301) 555-4174 | 7526138472 | 6P58WS2
--4328GD8 | 10 | 19 | Danielle | (389) 555-5198 | 8496433585 | 4328GD8. *********************
--G412CB7 | 10 | 20 | Roger | (130) 555-0289 | 1695452385 | G412CB7.  **************************-
--L93JTIZ | 10 | 21 | Elizabeth | (829) 555-5269 | 7049073643 | L93JTIZ
--322W7JE | 10 | 23 | Russell | (770) 555-1861 | 3592750733 | 322W7JE.  *********************
--0NTHK55 | 10 | 23 | Evelyn | (499) 555-9472 | 8294398571 | 0NTHK55.  ********************

--7
--SELECT  *
--FROM people join bank_accounts on people.id = bank_accounts.person_id

-- after that we compare the phone number esulted before:
--caller.        | receiver       | day| month | year | duration
--(130) 555-0289 | (996) 555-8899 | 28 | 7 | 2020 | 51. ************** G412CB7.         ######################
--(499) 555-9472 | (892) 555-8872 | 28 | 7 | 2020 | 36. ************** 0NTHK55.    duplicated.  #####################
--(367) 555-5533 | (375) 555-8161 | 28 | 7 | 2020 | 45. ************** 94KL13X.                            include in people and bank
--(609) 555-5876 | (389) 555-5198 | 28 | 7 | 2020 | 60. ************** 4328GD8.      receiver.           include in people andbank
--(499) 555-9472 | (717) 555-1342 | 28 | 7 | 2020 | 50. ************** 0NTHK55.    duplicated.   #####################
--(286) 555-6063 | (676) 555-6554 | 28 | 7 | 2020 | 43
--(770) 555-1861 | (725) 555-3243 | 28 | 7 | 2020 | 49. ************** 322W7JE.                        include in poeple and bank
--(031) 555-6622 | (910) 555-3251 | 28 | 7 | 2020 | 38
--(826) 555-1652 | (066) 555-9701 | 28 | 7 | 2020 | 55
--(338) 555-6650 | (704) 555-2131 | 28 | 7 | 2020 | 54


--8
--select *
--from passengers

--flight_id | passport_number | seat
--11 | 8496433585 | 5D
--18 | 3592750733 | 4C
--24 | 3592750733 | 2C
--36 | 5773159633 | 4A.       ***** meme id et 29/7/2020
--36 | 8496433585 | 7B.       *****
--48 | 8496433585 | 7C
--54 | 3592750733 | 6C

-- we filtering the passport number for the next day of crime (29/7/2020)

--9
--select*
--from flights join passengers on flights.id = passengers.flight_id
--where day = 28 and month = 7 and year = 2020

--id | name | phone_number | passport_number | license_plate | account_number | person_id | creation_year | flight_id
--  ***************686048 | Ernest | (367) 555-5533 | 5773159633 | 94KL13X | 49610011 | 686048 | 2010.               caller.|| 36-4A.  theif
--   *************467400 | Danielle | (389) 555-5198 | 8496433585 | 4328GD8 | 28500762 | 467400 | 2014.             receiver|| 11-5D / 36-7B / 48-7C
--514354 | Russell | (770) 555-1861 | 3592750733 | 322W7JE | 26013199 | 514354 | 2012.              caller. || 18-4C / 24-2C / 54-6C


--10
--select *
--from flights join airports on airports.id = flights.origin_airport_id


-- after this we compare the original and destination iairports id from fiftyville to the city


--id | abbreviation | full_name | city

--4 | LHR | Heathrow Airport | London
--8 | CSF | Fiftyville Regional Airport | Fiftyville






-- finaly, we limit the range of name and city to two person and one origne airport , one destination airport

-- in the final analyse :

-- the theif is : is the caller , Ernest
-- the theif's accomplie is : the receiver , Danielle
-- the city who the theif escaped to is : the destination airport , London

```

</br>
</br>
