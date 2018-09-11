
Why Hazelcast, Because it is clustered, It Implements JSR 107, Supports JCache.
-- Hazelcast is in memory Caching solution it usase inmemory Data grid.
-- Hazelcast is written in Java.
-- Easy to implement have enoroums support for Spring and hibernate.
https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-caching.html 


Deploying Application On Oracle.
Setup Your Oracle DB.

docker pull sath89/oracle-12c
docker run --name oracleDB -p 127.0.0.1:5500:5500 -p 127.0.0.1:1521:1521 sath89/oracle-12c
docker start oracleDB

docker exec -it oracleDB bin/bash
root@eb368f64b8d5:/# sqlplus

Enter user-name: system
Enter password: oracle

Sql Scripts to be executed.


Create Table.
create table ticket (ticket_id number,booking_date date,destination_station varchar2(255),email varchar2(255),passenger_name varchar2(255),source_station varchar2(255));

--Insert Scripts.
INSERT INTO "TICKET" ("TICKET_ID", "BOOKING_DATE", "DESTINATION_STATION", "EMAIL", "PASSENGER_NAME", "SOURCE_STATION") VALUES ((SELECT MAX(TICKET_ID)+ 1 FROM TICKET ) , TO_DATE('2017-07-19 11:41:36', 'YYYY-MM-DD HH24:MI:SS'), 'PUNE', 'KUMAR.ABHISHEK0809@GMAIL.COM', 'KUMAR', 'DELHI');

----------------------------------------------------------------------------------
pushing the jar file on docker hub. gradle buildDocker -Ppush

--pushing file on local docker.
--the port is same like in your docker file.
#For multiple servers.
#Change  into Dockerfile for port.
gradle clean build
docker build -f /home/vaishnavi/IdeaProjects/hazelcast-client/src/main/docker/Dockerfile -t hazelcast-client .


#Linking container.
docker run --name hazelcast-client-9191 -p  9191:9191 --link oracleDB:oracleDB -e SPRING_DATASOURCE_URL=jdbc:oracle:thin:@oracleDB:1521:xe -e SERVER_PORT=9191 hazelcast-client

docker run --name hazelcast-client-9191 -p  9191:9191 --link oracleDB:oracleDB -e SPRING_DATASOURCE_URL=jdbc:oracle:thin:@oracleDB:1521:xe -e SERVER_PORT=9191 hazelcast-client

docker run --name hazelcast-client-9191 -p  9191:9191 --link oracleDB:oracleDB -e SPRING_DATASOURCE_URL=jdbc:oracle:thin:@oracleDB:1521:xe -e SERVER_PORT=9191 hazelcast-client


https://hub.docker.com/r/hazelcast/hazelcast/
docker pull hazelcast/hazelcast

docker run -d --name hazelcast-5701 -p 127.0.0.1:5701:5701 hazelcast/hazelcast

#References 
http://localhost:32774/hazelcast-mancenter/login.html
https://stackoverflow.com/questions/20385973/how-do-you-programmatically-configure-hazelcast-for-the-multicast-discovery-mech
--Intializing Hazel Cast.
https://www.youtube.com/watch?v=-_OY-cI0WO4


----------------------------------------------------------------------------------
API 
getTicketById::
http://localhost:9192/api/tickets/ticket/{ticketId}
----------------------------------------------------------------------------------
deleteTicket::
http://localhost:9192/api/tickets/ticket/{ticketId}
----------------------------------------------------------------------------------
updateTicket::
http://localhost:9192/api/tickets/ticket/{ticketId}/{newEmail:.+}
