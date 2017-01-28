# Library Management System (LMS) for a university

## Technologies
Spring, DI, AOP, MVC, ORM, transactions.

## Tools
IntelliJ, Maven, MySQL, Jenkins, Apache Tomcat

## Requirements implemented

### Functional Requirements
This app manages many aspects of a university library system, including cataloging, search, circulation, and waiting list. The interface is web based, and the server needs to be hosted on the cloud, and is accessible from anywhere with Internet connection.

#### Users and Authentication
There are two roles of users, librarian and patron.

1. A librarian manages cataloging, and can assist circulation as well.

2. A patron is a customer of the library. He can search for books, borrow and returns books.

3. For simplicity, we allow any user with any email address to be able to create his account using an email as the username, and password of his choice. The user also needs to provide a university ID of 6 digits.

4. App sends an email to the user with a verification code. The user needs to use that verification code to complete his account registration. A registered user cannot really use features in the system until his account is verified. A confirmation email must be sent to the user after completion of account verification.

5. For simplicity, we only and automatically register any user with an SJSU email account (@sjsu.edu) to be a librarian.  A librarian cannot be a patron, which means he has to use a different email to register if he needs a patron account as well.

6. No two patrons can have the same university ID, neither can two librarians.

#### Cataloging

1. A librarian is able to manage the catalog of the books.

2. A book item contains the following properties 

  * Author
  * Title
  * Call number
  * Publisher
  * Year of publication
  * Location in the library;
  * Number of copies
  * Current status
  * Keywords
  * Coverage image

3. A librarian is able to search, add, update, and delete books.

  * Search capability functions as a superset of search features to be described below for patrons.  
    * Search has the apability to search for books created or updated by a particular librarian.  
  * Update and deletion works together with search, i.e., a librarian has the capability to find a book through search, then decide to update/delete it.
  * A book cannot be deleted if it’s checked out by a patron.
  * Deleting a book also removes the waiting list for it, if there is any.
  * [Bonus Feature] Integrated with external APIs to simplify the input the book info based on ISBN.

#### Circulation
1. A patron is able to check out up to 5 books in any day. 
    1. Each check out transaction can handle up to 5 books. 
    2. A book is due in 30 days from checking out.
    3. The checkout screen shows the due date.
    4. A confirmation email is sent to the patron for each checkout transaction with the details, including the book info, the transaction date and time, and the due day.
2. The total number of books a user can keep at any given time cannot exceed 10.
3. If a book is due within 5 days, daily alerts will be sent to the patron; and the patron can renew the book for another 30 days before the book is overdue. A book can be renewed twice, which means a maximum of 90 days in total from checked out. If, however, there is a waiting list for the book, it can no longer be renewed.   
4. A patron is able to return up to 10 books in one transaction. 
  1. Upon returning, an email confirmation is sent to the patron with the detail of the transaction.
  2. If any book is overdue, a fine of $1 per day is enforced.
  3. If the overdue period is not more than 24 hours, it is counted as one day
  4. If it is more than 24 hours, but not more than 48, it is counted as two days. So on and so forth. 

#### Waiting list
1. A patron can add himself to a waiting list if the book he is interested in is currently checked out by somebody else. There is no limit on how many people can be added to a waiting list, yet the order in the waiting is preserved. You cannot add the same person to the same list twice for the same book.
2. When a book becomes available, the first person on the waiting list is notified about its availability, and the person is removed from the waiting list. The book is reserved for this person for three days, during which only this person can check out this book. After these three days, the reservation is cancelled, and the next person in the waiting list (if there is any) is notified about the availability, and a three-day reservation is created for him as well. So on and so forth.

#### Testing Assistance
For ease of testing, the capability for a librarian to set the current date and time for the app has been provided. This way it is easier to test features like due date and waiting lists.  This interface for setting the date and time has been positioned at the top right corner of the main UI pages, and the resulted date and time is clearly displayed along with the time setting interface as well.

## Github setup
1. Use a github UI application. E.g. Source Tree
2. Clone this repository to your workstation: https://github.com/shubhamvadhera/library-management-spring
3. Follow the instructions from this document to setup the environment on your local machine.

## Google Cloud - Compute Engine Connectivity
1. Create a new ssh key-pair to connect to the Cloud machine. Instructions: https://cloud.google.com/compute/docs/instances/connecting-to-instance#generatesshkeypair
2. Login to your cloud console via ssh. 
  * Linux/Mac: https://cloud.google.com/compute/docs/instances/connecting-to-instance#standardssh 
  * Windows: https://cloud.google.com/compute/docs/instances/connecting-to-instance#putty

## Push to build with Jenkins
We used Jenkins for automatic builds on the server. Whenever some new code is pushed onto the master branch Jenkins will pull the commit and start the build.
Maven is the choice of build tool.

## Using Jenkins
Start Jenkins Server with command: java -jar jenkins.war --httpPort=9090

## Contributors:
Skanda Bhargav

Sagar Dafle

Dhanya Ramesh

Shubham Vadhera
