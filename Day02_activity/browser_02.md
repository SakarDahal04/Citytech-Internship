@startuml
' --- Spacing and Styling ---
skinparam BoxPadding 30
skinparam ParticipantPadding 40
skinparam monochrome true
skinparam shadowing false
skinparam DefaultTextAlignment center

|Network Thread|
start
:Receive HTTP Response;

|#Lavender|Engine|
fork
  |HTML Parser|
  :Tokenize HTML;
  :Build **DOM Tree**;
fork again
  |CSS Parser|
  :Fetch External CSS;
  :Build **CSSOM Tree**;
end fork

|Render Tree Construction|
:Combine DOM + CSSOM;
:Create **Render Tree**;

|Layout Engine|
:Calculate Geometry (Reflow);

|Painting|
:Rasterization (Pixels);

|Browser UI|
:Display Final Pixels;
stop
@enduml