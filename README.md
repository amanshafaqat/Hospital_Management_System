Hospital Management System
📌 Project Description:
This project is a Hospital Management System developed in C++ to simulate real-world hospital operations such as managing hospitals, doctors, patients, and nurse availability.
The system allows users to add, remove, and display hospitals, doctors, and patients. It also manages patient admissions and discharges, keeps track of assigned doctors, and supports sorting hospitals based on their ratings. 
Additionally, the system includes a basic graph structure to represent network connections between hospital entities.

🛠️ Technologies Used:
The project is written in C++ using object-oriented programming concepts. 
It utilizes STL containers like vector, list, queue, and unordered_map to manage data efficiently.
It also implements a priority queue to maintain a min-heap of hospitals and a graph using an adjacency list for connectivity between entities.

📁 Features:
Hospital Management: Add, remove, and display hospital details including name, location, available beds, rating, contact, price per bed, number of doctors and nurses, and nurse availability.

Doctor Management: Add doctors to hospitals with their name, availability time, contact number, and degree. Display complete doctor data.

Patient Management: Add patients with name, ID, contact number, booking price, and assigned doctor ID. Remove and display patient data.

Patient Admission & Discharge: Admit and discharge patients to and from hospitals.

Graph Management: Add edges to represent connectivity and print the graph using an adjacency list.

Hospital Sorting: Sort hospitals based on their rating in descending order and display the sorted list.
