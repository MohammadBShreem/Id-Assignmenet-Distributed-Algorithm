# Id-Assignmenet-Distributed-Algorithm

authors:
  * [Mohammad SHREM](https://www.linkedin.com/in/mohammadbshreem/) <mohammad.shrem@edu.univ-fcomte.fr>
  * [Mariam AL KHALAF]() <mariam.al_khalaf@edu.univ-fcomte.fr>
  * [Idrissa MASSALY]() <idrissa.massaly@edu.univ-fcomte.fr>

supervisor:
  * [Abdallah Makhoul](https://www.femto-st.fr/en/femto-people/amakhoul) <abdallah.makhoul@univ-fcomte.fr>

project relaized in [VisibleSim](https://github.com/VisibleSim/VisibleSim)

---

# Id Assignment Distributed Algorithm

This project implements a distributed algorithm to assign unique IDs to nodes in a network using a logical tree structure. The algorithm proceeds in multiple phases to build the tree, calculate subtree sizes, and assign IDs while maintaining efficiency and robustness in a distributed environment.

---

## **Overview**

### **Purpose**
- Assign unique IDs to nodes (modules) in a distributed network.
- Build a logical tree structure starting from a designated leader module.

### **Components**
- **Leader Node**: Initiates the process and coordinates the tree-building and ID assignment.
- **Child Nodes**: Participate in building the tree and receive IDs from their parent.
- **Messages**: Used for inter-node communication (e.g., explore, confirm child, report size, assign ID).

### **Phases**
1. **Phase 1**: Build a logical tree structure.
2. **Phase 2**: Calculate the size of each node's subtree.
3. **Phase 3**: Assign unique IDs based on subtree sizes.

---

## **Algorithm Details**

### **Phase 1: Explore and Build the Tree**
- **Startup**:
  - The leader initiates the exploration phase by sending `TYPE_1_EXPLORE` messages to all neighbors.
- **Explore Neighbors**:
  - Nodes receiving an `Explore` message:
    - Accept or reject a sender based on whether they have already been discovered.
    - Confirm parent-child relationships with `TYPE_2_CONFIRM_CHILD` or `TYPE_3_REJECT_CHILD` messages.
- **Confirm Child**:
  - Nodes add the sender to their list of child modules.

### **Phase 2: Report Subtree Size**
- Each node calculates the size of its subtree by aggregating sizes reported by children.
- The sizes are propagated up to the leader using `TYPE_4_REPORT_SIZE` messages.

### **Phase 3: Unique ID Assignment**
- IDs are assigned starting from the leader.
- Each node propagates IDs to its children using `TYPE_5_ASSIGN_ID` messages, ensuring unique assignment.

---

## **Class Breakdown**

### **Constructor**
Initializes the object and registers message types with their respective handlers.

### **Methods**

#### **Tree Building**
- `startup()`: Starts the exploration phase if the node is a leader.
- `exploreNeighbors()`: Handles incoming exploration messages.
- `confirmChild()`: Confirms a child relationship.
- `rejectChild()`: Rejects a child relationship.

#### **Subtree Size Reporting**
- `reportSize()`: Handles size reports from children.
- `CHECK_SubtreeSize()`: Verifies if all size reports have been received.

#### **ID Assignment**
- `assignId()`: Assigns unique IDs to nodes.
- `CHECK()`: Handles the propagation of IDs to children.

#### **Utility Methods**
- `onInterfaceDraw()`: Displays the unique ID and subtree size of the node.
- `parseUserBlockElements()`: Parses configuration to determine if a node is the leader.

---

## **Message Types**
1. **`TYPE_1_EXPLORE`**: Initiates tree exploration.
2. **`TYPE_2_CONFIRM_CHILD`**: Confirms a child relationship.
3. **`TYPE_3_REJECT_CHILD`**: Rejects a child relationship.
4. **`TYPE_4_REPORT_SIZE`**: Reports subtree size.
5. **`TYPE_5_ASSIGN_ID`**: Assigns a unique ID.

---

## **Key Variables**
- **`uniqueID`**: Stores the node's unique ID after assignment.
- **`subtreeSize`**: Tracks the size of the subtree rooted at the node.
- **`isDiscovered`**: Marks whether the node has been discovered during exploration.
- **`parentModule`**: Pointer to the parent node.
- **`childrenModules`**: List of pointers to child nodes.
- **`childrenSizes`**: Tracks the sizes of the subtrees of each child.

---

## **How It Works**

1. **Leader Initialization**:
   - The leader starts the exploration process, sending messages to neighbors.

2. **Tree Construction**:
   - Nodes discover neighbors and establish parent-child relationships.

3. **Subtree Size Reporting**:
   - Each node computes its subtree size and reports it to its parent.

4. **Unique ID Assignment**:
   - IDs are assigned starting from the leader, ensuring no duplication.
     

<div align="center">
<img src="https://github.com/user-attachments/assets/459ca200-16d8-4fab-ba70-addc2a70f159"></br>
</div>

<div align="center">
<img src="https://github.com/user-attachments/assets/d6d8eb3b-75ec-447e-96de-dec795c773bf"></br>
</div>
  

---
