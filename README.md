#include <iostream>
#include <string>
#include <cmath>
#include <cstdlib>  // for strtoll

using namespace std;

// Function to decode the value from the given base
long long decodeValue(const string& value, int base) {
    return strtoll(value.c_str(), nullptr, base);  // Convert value in the given base to an integer
}

// Function to perform Lagrange Interpolation
double lagrangeInterpolation(int x[], long long y[], int n) {
    double result = 0;

    for (int i = 0; i < n; i++) {
        double term = y[i];
        for (int j = 0; j < n; j++) {
            if (i != j) {
                term *= (0 - x[j]) / (double)(x[i] - x[j]);
            }
        }
        result += term;
    }

    return result;
}

int main() {
    // First test case data
    int n1 = 4;
    int k1 = 3;
    int x1[] = {1, 2, 3, 6};  // The keys
    long long y1[] = { 
        decodeValue("4", 10),      // y1 decoded from base 10
        decodeValue("111", 2),     // y2 decoded from base 2
        decodeValue("12", 10),     // y3 decoded from base 10
        decodeValue("213", 4)      // y6 decoded from base 4
    };

    // Second test case data
    int n2 = 9;
    int k2 = 6;
    int x2[] = {1, 2, 3, 4, 5, 6, 7, 8, 9};  // The keys
    long long y2[] = {
        decodeValue("28735619723837", 10),    // y1 decoded from base 10
        decodeValue("1A22867F0CA", 16),       // y2 decoded from base 16
        decodeValue("32811A4AA0B7B", 12),     // y3 decoded from base 12
        decodeValue("917978721331A", 11),     // y4 decoded from base 11
        decodeValue("1A22886782E1", 16),      // y5 decoded from base 16
        decodeValue("28735619654702", 10),    // y6 decoded from base 10
        decodeValue("71AB5070CC4B", 14),      // y7 decoded from base 14
        decodeValue("122662581541670", 9),    // y8 decoded from base 9
        decodeValue("642121030037605", 8)     // y9 decoded from base 8
    };

    // Finding the constant term (c) for both test cases
    double c1 = lagrangeInterpolation(x1, y1, n1);
    double c2 = lagrangeInterpolation(x2, y2, n2);

    // Output the results
    cout << "The constant term (c) for the first test case is: " << c1 << endl;
    cout << "The constant term (c) for the second test case is: " << c2 << endl;

    return 0;
}
