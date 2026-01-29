@startuml
skinparam handwritten false
skinparam monochrome true

|Client|
start
:Enter URL in Browser;
:Construct HTTP Request;
:Send Request;

|Network / Transport Layer|
:Establish TCP Connection (3-way handshake);
:Segment Data into Packets;
:Route Packets to Server IP;

|HTTP Server (e.g., Nginx/Apache)|
:Receive Raw Packets;
:Reassemble HTTP Request;
:Check Cache/Static Files;
if (Is Request Dynamic?) then (yes)
  :Forward to Application;
else (no)
  :Retrieve Static Resource;
  goto response
endif

|Application Logic|
:Parse Headers & Body;
:Route to Controller;
:Apply Business Rules;
:Request Data;

|Data Store (DB)|
:Execute Query;
:Return Result Set;

|Application Logic|
:Format Response (JSON/HTML);
:Send to Web Server;

|HTTP Server (e.g., Nginx/Apache)|
label response
:Add Response Headers;
:Compress Content (Gzip);

|Network / Transport Layer|
:Transmit Data Packets;

|Client|
:Receive Response;
:Render Content;
stop
@enduml