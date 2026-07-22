The **DYNALOG** project is part of the field of intralogistics and warehouse automation, where mobile robots meet companies’ needs for flexibility and performance. Specifically, the project focuses on evaluating FIVES XCELLA’s solution, in which order fulfillment is handled by a fleet of AGVs capable of navigating and accessing warehouse racks via a system of elevators to retrieve or deposit packages. This is a “case picking” solution, a method that involves picking a complete case of a product (bin or package) rather than a single unit, either to be stored in the warehouse or to assemble an outbound order (pallet).

This solution highlights the importance of inventory management, as well as task scheduling and the selection of AGV routes.

![image](../images/Xcella.jpg)

# Warehouse Modeling
The warehouses in the FIVES XCELLA solution organize product inventory into aisles with levels featuring elevators for ascending on one side and descending on the other. These levels are themselves organized into racks—units containing a certain number of storage locations for packages. Each bay is separated by shelf supports.

In addition to the storage area, there is a floor space dedicated to order picking and order preparation. Depalletizing robots place packages to be stored onto conveyors so that AGVs can retrieve them at collection points (IN Bases). Similarly, palletizing robots retrieve packages to be removed from inventory onto conveyors, which are fed by packages deposited by the AGVs at drop-off points (Bases OUT). We assume that the overall inbound and outbound throughput rates are equal, such that the average number of products in inventory remains constant.

The AGVs can move through the warehouse by traveling on the floor, using elevators (Xcalator) to access upper levels, and traveling on rails. All movements permitted by the AGVs are modeled as a directed graph. The nodes of the graph represent points of interest on the floor or within the warehouse.

# Glossary

To ensure clear communication and shared understanding among all stakeholders, this section provides definitions of key terms and parameters used throughout the problem description. 


|      **Key terms**               |                                      **Definition**                                                          | 
| :------------------------------: | :----------------------------------------------------------------------------------------------------------: | 
|  Stock                           | A system of racks organized into aisles, levels, and bays (each aisle has N bays) for storing bins           | 
|  Tubes                           | Horizontal levels of the storage racks, which serve as the AGV traffic lanes on each floor                   | 
|  Baies                           | Furniture organizing the aisles: grouping storage locations. Each bay has 5 storage locations per level (nodes) accessible from the central tube (on the corresponding level)       |
|  Location                        | A storage location capable of holding one bin or package, accessible from a position within a tube (node), to the right or left across two levels of depth                             |
|  Container / package / Bin       | Individual containers stored in locations, each dedicated to a single item number                            |
|  Product reference (SKU)         | A unique item reference used to identify the contents of a bin. A bin can contain only one reference, but multiple stock locations may have the same reference (redundancy). Example: reference “597631” for “Evian water packs.”                                                        |
|  Upward Elevator: Xcalator IN    |  An elevator at the entrance to the aisle that allows AGVs to travel up to the tubes.                        |
|  Downward elevator: Xcalator OUT | A lift at the end of the aisle that allows AGVs to return to ground level                                    |
|  Base IN                         |  Collection point where AGVs pick up bins to be put into stock from a picking station                        |
|  Base OUT                        |  Drop-off point where AGVs deposit bins to be removed from inventory at a Depose Station                     |
|  Picking Stations IN             |  All IN bases and infeed conveyors associated with a depalletizing robot                                     |
|  OUT Drop-Off Stations           |  All OUT bases and exit conveyors associated with a palletizing robot                                        |
|  Consistent palette              |  Pallet consisting of bins with the same part number                                                         |
|  Mixed Pallet                    | Pallet consisting of bins containing items with different part numbers                                       |
|  Depalletizing Robot             | Depalletizes homogeneous pallets and places the bins onto one or more conveyors feeding the IN Bases         |
| Palletizing Robot                | Creates mixed pallets from bins coming from one or more conveyors fed by the OUT Stations                    |
| AGV                              | Autonomous mobile robot responsible for transporting bins within the warehouse                               |


