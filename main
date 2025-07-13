#include <iostream>
#include <vector>
#include <list>
#include <queue>
#include <unordered_map>
#include <algorithm>

using namespace std;

class Doctor {
public:
    string doctor_name;
    string availability_time;
    string contact_number;
    string degree;
};

class Hospital {
public:
    string H_name;
    string location;
    int available_beds;
    float rating;
    string contact;
    int price;

    vector<Doctor> doctors;
    int num_doctors;

    int num_nurses;
    string nurses_availability;

    list<int> patients_ids;

    Hospital(const string& name, const string& loc, int beds, float rat, const string& cont, int pri, int doc, int nur, const string& nur_availability)
        : H_name(name), location(loc), available_beds(beds), rating(rat), contact(cont), price(pri), num_doctors(doc), num_nurses(nur), nurses_availability(nur_availability) {}
};

class Patient {
public:
    string P_name;
    int P_id;
    string contact;
    int price;
    int assigned_doctor_id;

    Patient(const string& name, int id, const string& cont, int pri, int doc_id)
        : P_name(name), P_id(id), contact(cont), price(pri), assigned_doctor_id(doc_id) {}
};

class Graph {
public:
    unordered_map<int, vector<int>> adjacencyList;

    void addEdge(int u, int v) {
        adjacencyList[u].push_back(v);
        adjacencyList[v].push_back(u);
    }

    void printGraph() {
        cout << "PRINT GRAPH:" << endl;
        for (const auto& [node, neighbors] : adjacencyList) {
            cout << "Node " << node << " is connected to: ";
            for (int neighbor : neighbors) {
                cout << neighbor << " ";
            }
            cout << endl;
        }
        cout << endl;
    }
};

class HospitalManagementSystem {
private:
    unordered_map<int, Hospital> hospitalMap;
    list<Patient> patientList;
    priority_queue<Hospital, vector<Hospital>, greater<Hospital>> minHeap;

public:
    // Hospital functions
    void addHospital(int id, const Hospital& hospital) {
        hospitalMap[id] = hospital;
        minHeap.push(hospital);
    }

    void removeHospital(int id) {
        hospitalMap.erase(id);
        rebuildMinHeap();
    }

    void printHospitalData() {
        cout << "PRINT hospitals DATA:" << endl;
        cout << "HospitalID   HospitalName     Location     Beds_Available     Rating     Hospital_Contact     Price_Per_Bed     Num_Doctors     Num_Nurses     Nurses_Availability    \n";

        for (const auto& [id, hospital] : hospitalMap) {
            cout << id << "             "
                 << hospital.H_name << "                  "
                 << hospital.location << "           " << hospital.available_beds << "                    "
                 << hospital.rating << "            " << hospital.contact << "             "
                 << hospital.price << "            "
                 << hospital.num_doctors << "               "
                 << hospital.num_nurses << "               "
                 << hospital.nurses_availability << "               "
                 << endl;
        }
        cout << endl << endl;
    }

    int getAvailableDoctorId(int hospitalId) {
        if (hospitalMap[hospitalId].doctors.size() > 0) {
            int doctorId = hospitalMap[hospitalId].doctors.size();
            return doctorId;
        }
        return -1; // No available doctor
    }

    void admitPatientToHospital(int patientId, int hospitalId) {
        hospitalMap[hospitalId].patients_ids.push_back(patientId);
    }

    void dischargePatientFromHospital(int patientId, int hospitalId) {
        hospitalMap[hospitalId].patients_ids.remove(patientId);
    }

    // Doctor functions
    void addDoctor(int hospitalId, const Doctor& doctor) {
        hospitalMap[hospitalId].doctors.push_back(doctor);
        hospitalMap[hospitalId].num_doctors++;
    }

    void printDoctorData(int hospitalId) {
        cout << "PRINT doctors DATA:" << endl;
        cout << "DoctorID   DoctorName     AvailabilityTime     ContactNumber     Degree     \n";

        int doctorId = 1;
        for (const auto& doctor : hospitalMap[hospitalId].doctors) {
            cout << doctorId << "             "
                 << doctor.doctor_name << "                  "
                 << doctor.availability_time << "           " << doctor.contact_number << "                    "
                 << doctor.degree << "            "
                 << endl;
            doctorId++;
        }
        cout << endl << endl;
    }

    // Patient functions
    void addPatient(const Patient& newPatient) {
        patientList.push_back(newPatient);
    }

    void removePatient(int patientId) {
        patientList.remove_if([patientId](const Patient& p) { return p.P_id == patientId; });
    }

    void printPatientData() {
        cout << "PRINT patients DATA:" << endl;
        cout << "PatientName     PatientID     Contact     BookingCost     AssignedDoctorID     \n";

        for (const auto& patient : patientList) {
            cout << patient.P_name << "                  "
                 << patient.P_id << "       " << patient.contact << "           " << patient.price << "            "
                 << patient.assigned_doctor_id << "            "
                 << endl;
        }
        cout << endl << endl;
    }

    // Graph functions
    void addEdgeToGraph(int u, int v, Graph& graph) {
        graph.addEdge(u, v);
    }

    void printGraph(Graph& graph) {
        graph.printGraph();
    }

    // Sorting and Heap functions
    void rebuildMinHeap() {
        priority_queue<Hospital, vector<Hospital>, greater<Hospital>> newHeap;
        for (const auto& entry : hospitalMap) {
            newHeap.push(entry.second);
        }
        minHeap = newHeap;
    }

    void sortHospitalsByRating() {
        vector<pair<int, Hospital>> sortedHospitals;
        for (const auto& [id, hospital] : hospitalMap) {
            sortedHospitals.push_back({id, hospital});
        }
        sort(sortedHospitals.begin(), sortedHospitals.end(), [](const auto& a, const auto& b) {
            return a.second.rating > b.second.rating;
        });

        cout << "Sorted Hospitals by Rating:" << endl;
        for (const auto& [id, hospital] : sortedHospitals) {
            cout << id << ": " << hospital.H_name << " - Rating: " << hospital.rating << endl;
        }
        cout << endl;
    }
};

int main() {
    HospitalManagementSystem system;
    Graph graph;

    // User Input
    int hospitalId, doctorHospitalId, patientHospitalId, patientDoctorId, u, v;

    // Add hospitals
    cout << "Enter Hospital ID: ";
    cin >> hospitalId;
    Hospital hospital;
    // Get hospital details (name, location, beds, rating, contact, price, num_doctors, num_nurses, nurses_availability) - input validation not implemented for simplicity
    system.addHospital(hospitalId, hospital);

    // Add doctors
    cout << "Enter Hospital ID for adding a doctor: ";
    cin >> doctorHospitalId;
    Doctor doctor;
    // Get doctor details (doctor_name, availability_time, contact_number, degree) - input validation not implemented for simplicity
    system.addDoctor(doctorHospitalId, doctor);

    // Add patients
    Patient patient;
    // Get patient details (P_name, P_id, contact, price, assigned_doctor_id) - input validation not implemented for simplicity
    system.addPatient(patient);

    // Add edges to graph
    cout << "Enter edge (u, v) for the graph: ";
    cin >> u >> v;
    system.addEdgeToGraph(u, v, graph);

    // Admit patient to hospital
    cout << "Enter Patient ID and Hospital ID for admission: ";
    cin >> patientDoctorId >> patientHospitalId;
    system.admitPatientToHospital(patientDoctorId, patientHospitalId);

    // Discharge patient from hospital
    cout << "Enter Patient ID and Hospital ID for discharge: ";
    cin >> patientDoctorId >> patientHospitalId;
    system.dischargePatientFromHospital(patientDoctorId, patientHospitalId);

    // Remove hospital
    cout << "Enter Hospital ID for removal: ";
    cin >> hospitalId;
    system.removeHospital(hospitalId);

    // Remove patient
    cout << "Enter Patient ID for removal: ";
    cin >> patientDoctorId;
    system.removePatient(patientDoctorId);

    // Display data
    system.printHospitalData();
    system.printDoctorData(1);
    system.printPatientData();
    system.printGraph(graph);

    // Sorting and heap operations
    system.sortHospitalsByRating();

    return 0;
}
