### BEFORE STARTING:
Given the nature of remote resolution of the following exercises, it's easy for the applicant to cheat when solving them, but we really recommend approaching them honestly, because even if he pass the technical evaluation fraudulently, tomorrow he will have to demonstrate his knowledge in a real environment **where only real knowledge counts**. Good luck. Ivan.

> Note: the parts that say "**Extra**" are activities that, although they are not mandatory, applicants can complete to demonstrate that they have greater knowledge and increase their chances of accessing the position.

# Barry Allen Logistics

![Barry Allen Logistics](./flash.png)

_We have entered a new and thriving logistics-oriented company. This company is responsible for the transport of goods around the world and is in the process of digitizing its activities. We are the rookie so we must build a reputation._

Our first task is to write a sql query that feeds a report that allows the central office to know all the trips made. This report is expected to show, for each trip, the number of packages transported and the total amount of their fares. The results must be ordered from the newest to the oldest and must also exclude trips with more than 3 packages. Note: you should only write the query, not make the report.

> [https://www.mycompiler.io/view/1bXLimu](https://www.mycompiler.io/view/10K86HhhTMV) (you will need to fork it to edit it)

The next day we noticed that the backend team is a bit busy so we decided to show off our PHP knowledge and help them. They tell us that they need help with the destination search engine. These destinations are organized as a hierarchy in a tree and since they come from an external service that is always changing, they cannot count on the tree always having the same number of levels and the team ask us if we can implement the function that They need to search the tree. It receives as arguments, the tree with the destinations and the text to search for (in any part of the name).

> [https://phpsandbox.io/n/hhrr-search-into-tree-gbizl](https://phpsandbox.io/n/destination-search-vicif) (you will need to fork it to edit)

> **Extra**: Instead of searching by text you can receive the search criteria as a function (higher-order function)

Due to our good work the CTO of the company decides to put our JS skills to the test with a peculiar challenge. We are given a json that includes the issued invoices and we are asked to calculate the total due (of the unpaid invoices) by type of customer. It's a piece of cake... but we're not allowed to use loops (for, while, do while) or the forEach method. It is also not allowed to use recursion, Gulp.

> [https://replit.com/@IvanStadius/HHRR-Declaratividad#index.js](https://replit.com/@IvanStadius/HHRR-Declaratividad#index.js)(you will need to fork it to edit it)

Now, having proven our worth, we are allowed to play with the big boys. We are going to participate in the development of the application's core. The business rules are as follows:

* There is a "truck" entity, it has a **Truck Model** and a patent.
* Each **Truck Model** supports volume (m3) and maximum weight (kg)
* A **Roadmap** can be asigned to a **Truck**. Trucks can be assigned only one roadmap at a time.
* A **Roadmap** groups **Trips** AND OTHER **ROADMAPS**, they have n trips/roadmaps (it can have a combination).
* There are three types of **Trips**: Normal, Priority, Return.
* A **Trip** contains n **Packages**, a **Package** have weight (kg), height, width and length (m).
* A **Trip** contains an **Origin** and a **Destination**, these origins and destinations have address and coordinates (latitude and longitude)
* Roadmaps, trips and truck models are immutable, once created they are not modified.

It's our responsability to model these entities correctly using the principles of object-oriented programming (inheritance, composition, polymorphism, etc...) and **create a method that calculates the cost per roadmap**. Also if you try to load a roadmap on a truck that exceeds its capabilities, an exception must be thrown. 

The rules for calculating the value of a **Trip** are as follows:

* If the type of the **Trip** is **Normal**, the cost is $2 x Kg x KM
* If the type of the **Trip** is **Priority**, the cost is the higher of these two
    * $4 * Kg x KM
    * $10 * M3(volume) * KM
* If the type of the **Trip** is **Return**, a flat rate of $1000 is charged
* To calculate the kilometers traveled, the distance is calculated in a straight line between the origin and destination coordinates. To do that there are many functions on the internet, we leave one that you can use at the end of this document.

MANDATORY: Use typed php in the methods. Both for parameters and return values.

> This exercise can be done at https://phpsandbox.io or at the IDE of your choice

> **Extra**: Develop some unit tests, it is not necessary to have a great coverage, just demonstrate that you have the knowledge.

> **Bonus**: Use phpdoc to document

> **Bonus**: Create UML class diagram

## Delivery
* The delivery of the technical test is by email (to the same address from which the link to this repository was sent) and the code can be in:
    * The online IDEs supplied in which case we will only require the links.
    * A zip with all the files attached to the email.
    * A git repo

* It is not necessary to complete 100% of the test to send it, do as much as you can. Also **Extra** points are optional.



### Distance calculation


```
function getDistanceBetweenPoints(float $latitude1, float $longitude1, float $latitude2, float $longitude2) : float {
    $theta = $longitude1 - $longitude2;
    $distance = (sin(deg2rad($latitude1)) * sin(deg2rad($latitude2))) + (cos(deg2rad($latitude1)) * cos(deg2rad($latitude2)) * cos(deg2rad($theta)) );
    $distance = acos($distance);
    $distance = rad2deg($distance);
    $distance = $distance * 60 * 1.1515;
    $distance = $distance * 1.609344;
    return(round($distance,2));
}
```
