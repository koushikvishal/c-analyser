#include <iostream>
#include <vector>
#include <string>
#include <ctime> // for timing

using namespace std;

// Function to perform QuickSort on genomic sequences
void quickSort(vector<string>& sequences, int left, int right);

// Partition function to find pivot index
int partition(vector<string>& sequences, int left, int right);

// Function to display genomic sequences
void displaySequences(const vector<string>& sequences);

void quickSort(vector<string>& sequences, int left, int right) {
    if (left < right) {
        // Partition the array and get the pivot index
        int pivotIndex = partition(sequences, left, right);

        // Recursively sort the left and right subarrays
        quickSort(sequences, left, pivotIndex - 1);
        quickSort(sequences, pivotIndex + 1, right);
    }
}

int partition(vector<string>& sequences, int left, int right) {
    string pivot = sequences[right]; // Choose the last element as the pivot
    int i = left - 1; // Index of smaller element

    for (int j = left; j < right; j++) {
        // If the current element is smaller than or equal to the pivot
        if (sequences[j] <= pivot) {
            i++; // Increment index of smaller element
            // Swap sequences[i] and sequences[j]
            swap(sequences[i], sequences[j]);
        }
    }
    // Swap sequences[i+1] and sequences[right] (pivot)
    swap(sequences[i + 1], sequences[right]);
    return (i + 1); // Return the partition index
}

// Function to display genomic sequences
void displaySequences(const vector<string>& sequences) {
    cout << "Genomic Sequences:\n";
    for (const string& sequence : sequences) {
        cout << sequence << " ";
    }
    cout << endl;
}

int main() {
    // Input genomic sequences from the user
    int numSequences;
    cout << "Enter the number of genomic sequences: ";
    cin >> numSequences;

    vector<string> genomicSequences(numSequences);
    cout << "Enter the genomic sequences:\n";
    for (int i = 0; i < numSequences; ++i) {
        cin >> genomicSequences[i];
    }

    // Display unsorted genomic sequences
    displaySequences(genomicSequences);

    // Perform QuickSort on genomic sequences
    clock_t start = clock(); // Start the timer
    quickSort(genomicSequences, 0, genomicSequences.size() - 1);
    clock_t end = clock(); // End the timer

    // Display sorted genomic sequences
    displaySequences(genomicSequences);

    // Calculate and display the time taken for sorting
    double elapsedTime = double(end - start) / CLOCKS_PER_SEC;
    cout << "Time taken for sorting: " << elapsedTime << " seconds" << endl;

    return 0;
}
