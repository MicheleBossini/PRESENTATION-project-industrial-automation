# Interactions between the components
```plantuml
@startuml ExtrusionProcess
' Title of the diagram
title Extrusion and Material Processing Flow
skinparam ArrowThickness 1.5

skinparam component<<dashed>> {
    BorderStyle dashed
}
skinparam component<<Solid>> {
    BorderStyle LineThickness 6
}
package StartingMaterial as "Starting Material" {
  [Thermoplastic Material]
}
' Definitions of the main components
package Extruder {
  [Hot Material]
}
package HaulOff as "Haul-Off System" {
  [Pulling Mechanism]
}
package Press as "Press Machine"{
  [Pressing Cylinder]
  [Moving Rails]
  [Processing Area]

}

    component Synchronization_Bord <<dashed>>{
    [Speed]
    [Rail Position]
    [Cylinder]
    [Temperature Control]

}
    package Temperature_Control as "Temperature Control"{
    [Infrared Lamp]
    [Cooling System]
}

' Material flow and actions
[Thermoplastic Material] -> [Hot Material] : Material Processed
[Hot Material] --> [Pulling Mechanism] : **Extruded**
[Infrared Lamp] -up-> [Hot Material] : Keeping Temperature



' Movement and Processing of the Material
[Pulling Mechanism] --> [Processing Area] : Pulled Material

' Description of movements in the Press
[Processing Area] -down-> [Moving Rails] : **Input Position**
[Processing Area] -down-> [Pressing Cylinder] : **Pressing/Opening Action**

[Processing Area] --> [Processed Material] : Finished Material
note right of [Processing Area]
    The material is positioned into the press
    and pressed by the cylinder.
end note

' Legend
legend right
  - [] : State or Product
  - component : Machinery or System
  - --> : Process Flow
  - .> : Synchronization input/output
end legend
[Processed Material] <-up- [Cooling System] : **Pressing/Opening 

'Synchronization of the whole process
[Speed] ..> [Pulling Mechanism] : Pulled Material Speed
[Hot Material] ..> [Speed] : Pulled Material Speed
[Speed] ..> [Moving Rails] : Pulled Material Speed
[Rail Position] ..> [Moving Rails] : Initial/Final position
[Cylinder] ..> [Pressing Cylinder] : Pressing/Opening action
[Temperature Control] ..> [Infrared Lamp] : Temperature Manegement
[Temperature Control] ..> [Cooling System] : Temperature Manegement
@enduml
```


The synchronization bord is connected to all components of the machine and oversees the entire process, ensuring that all data flows through it. It controls and synchronizes every aspect of the operation.

Synchronization Control:
  - infrared lamp / cooling system
  - cylinder action
  - rail position and speed
  - haul-Off speed
  - Safety alarm
  - emergency stop