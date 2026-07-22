The **DYNALOG** project is part of the field of intralogistics and warehouse automation, where mobile robots meet companies’ needs for flexibility and performance. Specifically, the project focuses on evaluating FIVES XCELLA’s solution, in which order fulfillment is handled by a fleet of AGVs capable of navigating and accessing warehouse racks via a system of elevators to retrieve or deposit packages. This is a “case picking” solution, a method that involves picking a complete case of a product (bin or package) rather than a single unit, either to be stored in the warehouse or to assemble an outbound order (pallet).

This solution highlights the importance of inventory management, as well as task scheduling and the selection of AGV routes.

![image](../images/Xcella.jpg)

# Warehouse Description
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

# Modeling
Each edge of the graph represents a route that an AGV can take to move through the warehouse. An edge can be:
-    directed (traveled in only one direction), if it is on the warehouse floor;
-   undirected (traveled in both directions), if it is in the TUBES (storage levels)

And each node in the graph represents either a route intersection or a point of interest where an AGV can perform an ACTION.
An ACTION can be:
-    Picking up a package: either from an IN Base or from a location in a tube
-    Dropping off a package: either at an OUT Base or at a location in a tube
-    Attaching to an elevator (Xcalator)
-    Detach from an elevator (Xcalator)
-    Board an elevator (Xcalator) to go up to a tube level in the warehouse
-    Board an elevator (Xcalator) to go down to the ground floor
-    Move between two nodes in the graph
-    Change direction: along a curved path
-    Wait at a graph node

We distinguish between the warehouse ground level and the storage floor levels; in fact, each floor has only one path per aisle (TUBE), which simplifies the planning stage.

Next is a diagram of the different levels and components for a simple warehouse with:
-    Ten aisles and ten parallel routes per aisle beneath the storage area;
-    one depalletizing robot (picking station) with ten Base INs;
-    two palletizing robots (deposit stations) with two Base OUTs each;
-    ten bays per aisle, each with five slots (5 on the right and 5 on the left), with one depth for each slot.	

The following figure is a schematic representation of the warehouse - View of floor-level components. 
![image](../images/Schema.png)

The next figure is a schematic representation of the storage locations in each tube for each aisle.
![image](../images/Baies.png)

# System Constraints
In addition to the structural data provided above, the system imposes the following constraints:
- One AGV per Xcalator at a time;
-    Only one AGV per bay in the tubes, with a maximum of three AGVs per tube;
-    A bin can contain only one SKU, but multiple stock locations may have the same SKU (redundancy);
-    The order in which bins are sent to the palletizing conveyors must be followed;
-    A maximum of one AGV per graph node and a minimum distance of 10 cm between AGVs at all times (applies whether AGVs are following one another or crossing paths on two parallel routes)

# Data: Modeling and Generating Test Scenarios - Inventory and Missions
In order to test and compare the project’s various algorithms, it is necessary to formalize test datasets in the form of representative scenarios. These scenarios reflect two aspects in particular: the representation of a realistic warehouse inventory and the management of tasks to be performed by AGVs in the form of coherent missions. These dataset will be given to the contestants.

# Inventory and SKUs
To model realistic inventory, we consider two pieces of information about SKUs:
-     The presence of an SKU in inventory and in orders follows a “popularity” or skewness pattern. In other words, not every product has the same probability of being ordered; some products are more popular (in demand) and are therefore stocked in greater quantities.
-     Each SKU has weight/volume data that allows them to be sorted into three categories: M1 for the heaviest, M2 for medium, and M3 for the lightest. This category is used to organize outgoing pallets: packages containing SKUs in category M1 are placed first on the pallet, followed by M2, and then M3.
![image](../images/Stock.png)




