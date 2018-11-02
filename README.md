# spring-microservice

Steps to Execute:

Here we have config server its pulling the git file and servering the content to client.

We need not to update client or server we just call a curl command /actuator/refresh. autometically the updated values fetched on the client

We have 3 applications and one config file in the Git.

Build a config service application https://github.com/pradeeprkotha/spring-microservice

Zull proxy https://github.com/pradeeprkotha/proxy-gateway

Config client https://github.com/pradeeprkotha/spring-config-client

Config file https://github.com/pradeeprkotha/config-client

Client application is running on the 8989 port

Zull API gateway running on the port number 9090

Curl command to refresh the client curl localhost:8989/actuator/refresh -d {} -H "Content-Type: application/json".

Behind the scenes:

when we call http://localhost:9090/config-client/message

Response :a message from git repository on friday 953 IST

REST api will git Zull proxy
Proxy hits the Spring config application which is running on the port 8989
The client properties having the spring.cloud.config.uri=http://localhost:8888 in Service application the Git URL is spring.cloud.config.server.git.uri=https://github.com/pradeeprkotha/config-client.git Internally it will read the information and serves to the client dynamically.
When we update config file in git through a commit we have to call localhost:8989/actuator/refresh to fetch the new information. So dynamically the new values will be served in the client app. with out updating or restarting the Client/server.
