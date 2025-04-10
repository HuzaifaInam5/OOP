#include <iostream>
#include <string>
#include <vector>
#include <sstream>
using namespace std;

// Helper function to trim string (to avoid trailing whitespaces or newlines)
string trim(const string& str) {
    size_t first = str.find_first_not_of(" \t\n\r");
    size_t last = str.find_last_not_of(" \t\n\r");
    return (first == string::npos || last == string::npos) ? "" : str.substr(first, last - first + 1);
}

// Composition
class Corona {
    string name, address, age, gender, symptoms, tests, treatment, status;

public:
    Corona(string n, string a, string ag, string g, string s, string t, string tr, string st)
        : name(n), address(a), age(ag), gender(g), symptoms(s), tests(t), treatment(tr), status(st) {}

    string getName() const { return name; }
    string getAddress() const { return address; }
    string getAge() const { return age; }
    string getGender() const { return gender; }
    string getSymptoms() const { return symptoms; }
    string getTests() const { return tests; }
    string getTreatment() const { return treatment; }
    string getStatus() const { return status; }

    void setName(string val) { name = val; }
    void setAddress(string val) { address = val; }
    void setAge(string val) { age = val; }
    void setGender(string val) { gender = val; }
    void setSymptoms(string val) { symptoms = val; }
    void setTests(string val) { tests = val; }
    void setTreatment(string val) { treatment = val; }
    void setStatus(string val) { status = val; }
};

// Aggregation
class PatientDetails {
    Corona c;
    string id;

public:
    PatientDetails(string pid, Corona corona) : id(pid), c(corona) {}

    string getId() const {
        return id;
    }

    // Provide access to the `Corona` object
    Corona& getCorona() {  // Change: Return non-const reference for modification
        return c;
    }

    const Corona& getCorona() const {  // Keep const version for non-modifying access
        return c;
    }

    void displayDetails() const {
        cout << "Patient ID: " << id << endl;
        cout << "Patient Name: " << c.getName() << endl;
        cout << "Address: " << c.getAddress() << endl;
        cout << "Age: " << c.getAge() << endl;
        cout << "Gender: " << c.getGender() << endl;
        cout << "Symptoms: " << c.getSymptoms() << endl;
        cout << "Tests: " << c.getTests() << endl;
        cout << "Treatment: " << c.getTreatment() << endl;
        cout << "Status: " << c.getStatus() << endl;
    }
};

vector<PatientDetails> patients;  // In-memory list of patients

void addPatient() {
    string id, name, address, age, gender, symptoms, tests, treatment, status;
    cout << "Enter Patient ID: "; getline(cin, id);
    cout << "Enter Name: "; getline(cin, name);
    cout << "Enter Address: "; getline(cin, address);
    cout << "Enter Age: "; getline(cin, age);
    cout << "Enter Gender: "; getline(cin, gender);
    cout << "Enter Symptoms: "; getline(cin, symptoms);
    cout << "Enter Tests: "; getline(cin, tests);
    cout << "Enter Treatment: "; getline(cin, treatment);
    cout << "Enter Status: "; getline(cin, status);

    Corona corona(name, address, age, gender, symptoms, tests, treatment, status);
    PatientDetails patient(id, corona);
    patients.push_back(patient);

    cout << "Patient added successfully with ID: " << id << endl;
}

void viewPatient() {
    string id;
    cout << "Enter Patient ID to view: "; getline(cin, id);

    bool found = false;
    for (const auto& patient : patients) {
        if (trim(patient.getId()) == trim(id)) {
            patient.displayDetails();
            found = true;
            break;
        }
    }

    if (!found) {
        cout << "Patient ID not found." << endl;
    }
}

void updatePatient() {
    string id;
    cout << "Enter Patient ID to update: "; getline(cin, id);

    bool found = false;
    for (auto& patient : patients) {
        if (trim(patient.getId()) == trim(id)) {
            Corona& c = patient.getCorona();  // Access the Corona object as non-const for modification
            string input;

            cout << "Enter new Name (" << c.getName() << "): "; getline(cin, input); if (!input.empty()) c.setName(input);
            cout << "Enter new Address (" << c.getAddress() << "): "; getline(cin, input); if (!input.empty()) c.setAddress(input);
            cout << "Enter new Age (" << c.getAge() << "): "; getline(cin, input); if (!input.empty()) c.setAge(input);
            cout << "Enter new Gender (" << c.getGender() << "): "; getline(cin, input); if (!input.empty()) c.setGender(input);
            cout << "Enter new Symptoms (" << c.getSymptoms() << "): "; getline(cin, input); if (!input.empty()) c.setSymptoms(input);
            cout << "Enter new Tests (" << c.getTests() << "): "; getline(cin, input); if (!input.empty()) c.setTests(input);
            cout << "Enter new Treatment (" << c.getTreatment() << "): "; getline(cin, input); if (!input.empty()) c.setTreatment(input);
            cout << "Enter new Status (" << c.getStatus() << "): "; getline(cin, input); if (!input.empty()) c.setStatus(input);

            cout << "Patient record updated successfully." << endl;
            found = true;
            break;
        }
    }

    if (!found) {
        cout << "Patient ID not found." << endl;
    }
}

int main() {
    while (true) {
        cout << "\n----- COVID Patient Management System -----" << endl;
        cout << "1. Add New Patient" << endl;
        cout << "2. View Patient by ID" << endl;
        cout << "3. Update Patient by ID" << endl;
        cout << "4. Exit" << endl;
        cout << "Enter choice: ";
        string choice;
        getline(cin, choice);

        if (choice == "1") addPatient();
        else if (choice == "2") viewPatient();
        else if (choice == "3") updatePatient();
        else if (choice == "4") break;
        else cout << "Invalid choice. Please try again." << endl;
    }
    return 0;
}
