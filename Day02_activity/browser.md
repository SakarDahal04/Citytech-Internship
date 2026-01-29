@startuml
skinparam monochrome true
skinparam shadowing false

|Network Thread|
start
:Receive HTTP Response Body;
:Pass Data Stream to Renderer;

|HTML Parser|
:Tokenize HTML;
:Build **DOM Tree**;
if (Link to External CSS?) then (yes)
|CSS Parser|
  :Fetch CSS;
  :Build **CSSOM Tree**;
endif

|HTML Parser|
if (Script Tag Found?) then (yes)
|JavaScript Engine|
  :Fetch/Execute JS;
  :Modify DOM/CSSOM;
endif

|Render Tree Construction|
|HTML Parser|
:Combine DOM + CSSOM;
|Render Tree Construction|
:Create **Render Tree**;
note right: Filters out non-visual \nelements like <head>

|Layout Engine (Reflow)|
:Calculate Geometry;
note right: Determines size and \nposition of every node

|Painting & Compositing|
:Create Display List;
:Layering (Z-index);
:Rasterization (Pixels);

|Browser UI|
:Display Final Pixels on Screen;
stop
@enduml