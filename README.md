## 1 - The two microservices are running and registered (two terminals, logs screenshots)

### Screenshot one (Account Microservice running and registered)

Screenshot taken from IntelliJ Idea terminal:
![Account Microservice running and registered](https://raw.githubusercontent.com/piraces/Laboratory-6-microservices/master/screenshots/accountRunning.png)


### Screenshot two (WebService Microservice running and registered)

Screenshot taken from IntelliJ Idea terminal:
![WebService Microservice running and registered](https://raw.githubusercontent.com/piraces/Laboratory-6-microservices/master/screenshots/webServiceRunning.png)

## 2 - The service registration service has the two microservices registered (a third terminal, dashboard screenshots)

### Screenshot of Eureka Dashboard:

![Eureka Dashboard shows two microservices registered](https://raw.githubusercontent.com/piraces/Laboratory-6-microservices/master/screenshots/eurekaDashboard.png)

## 3 - A second account microservice is running in the port 4444 and it is registered (a fourth terminal, log screenshots)

### Screenshot four (Second Account microservice)

Screenshot taken from IntelliJ Idea terminal:
![Second Account microservice is running in the port 4444 and it is registered](https://raw.githubusercontent.com/piraces/Laboratory-6-microservices/master/screenshots/secondAccountRunning.png)

## 4 - A brief report describing what happens when you kill the microservice with port 2222.

### Can the web service provide information about the accounts? Why?

When you kill the Account microservice on port 2222, the WebService microservice, can't provide any information about the accounts. This is because it tries to contact to the Account microservice on port 2222 (which is dead), and shows "Refused connection" errors (because the service it's no longer available at this port). When the WebService microservice, knows that this microservice it's no longer available shows information messages such as "No instances available for ACCOUNTS-SERVICE". At last, it discover the other Account microservice on port 4444, and starts working normally and providing information about the accounts.

The explanation of all of it is the following:
When killed the Account microservice on port 2222, the WebService microservice, tries to contact it and fails with "Refused connection" (because it doesn't know the microservice is down). Later, it asks the service registration service for another microservice that provides the Account microservice. This service responds with the another microservice on port 4444, and then the Webservice microservice contact with it, and starts working and providing information again. All of these steps take a "minimal" time, but in seconds, it's working perfect again. The steps when the service realizes that the another service is dead and when it contact the another one, can be easily seen on the logs.
