#include <iostream>
#include <fstream>
#include <string>
#include "json.hpp"

using json = nlohmann::json;
using namespace std;

// Function to decode the base-specific value to base 10
long long decodeValue(int base, const string& value) {
    return stoll(value, nullptr, base); // Convert value string in base 'base' to base 10
}

int main() {
    // Open and parse the JSON file
    ifstream file("testcase1.json");
    json data;
    file >> data; // Parse JSON content from the file
    
    // Extract 'n' and 'k' from the "keys" section
    int n = data["keys"]["n"];   // Total number of roots
    int k = data["keys"]["k"];   // Minimum number of roots required
    
    cout << "Number of roots (n): " << n << endl;
    cout << "Minimum roots needed (k): " << k << endl;
    
    // Iterate through each root and decode the values
    for (int i = 1; i <= n; ++i) {
        int base = stoi(data[to_string(i)]["base"]); // Get base as integer
        string value = data[to_string(i)]["value"];  // Get encoded value
        
        // Decode the y-value from its base to base 10
        long long decodedY = decodeValue(base, value);
        
        // Display the decoded points
        cout << "Point " << i << " - Base: " << base << ", Decoded Y-value: " << decodedY << endl;
    }
    
    return 0;
}
