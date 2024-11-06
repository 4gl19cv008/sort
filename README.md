#include <stdio.h>

// Function prototypes
void quickSort(int arr[], int low, int high);
void selectionSort(int arr[], int size);
void heapSort(int arr[], int size);
void printArray(int arr[], int size);

// Function for partitioning in quickSort
int partition(int arr[], int low, int high);

// Main function (Engineer 1)
int main() {
    int arr[10], choice;
    int size = 10;

    // Input 10 numbers from the user
    printf("Enter 10 numbers: \n");
    for (int i = 0; i < size; i++) {
        scanf("%d", &arr[i]);
    }

    // Asking user to choose a sorting algorithm
    printf("Choose a sorting algorithm:\n");
    printf("1. Quick Sort\n");
    printf("2. Selection Sort\n");
    printf("3. Heap Sort\n");
    printf("Enter your choice (1-3): ");
    scanf("%d", &choice);

    // Printing the original array
    printf("Original Array: ");
    printArray(arr, size);

    // Calling the appropriate sorting function
    switch (choice) {
    case 1:
        quickSort(arr, 0, size - 1);
        printf("Array sorted with Quick Sort: ");
        break;
    case 2:
        selectionSort(arr, size);
        printf("Array sorted with Selection Sort: ");
        break;
    case 3:
        heapSort(arr, size);
        printf("Array sorted with Heap Sort: ");
        break;
    default:
        printf("Invalid choice!\n");
        return 1;
    }

    // Printing the sorted array
    printArray(arr, size);

    return 0;
}

// Function to print an array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// Quick Sort function (Engineer 2)
void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Partition function for Quick Sort
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;

    return (i + 1);
}

// Selection Sort function (Engineer 3)
void selectionSort(int arr[], int size) {
    for (int i = 0; i < size - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < size; j++) {
            if (arr[j] < arr[minIdx]) {
                minIdx = j;
            }
        }
        int temp = arr[minIdx];
        arr[minIdx] = arr[i];
        arr[i] = temp;
    }
}

// Heap Sort function (Engineer 4)
void heapSort(int arr[], int size) {
    // Build max heap
    for (int i = size / 2 - 1; i >= 0; i--) {
        heapify(arr, size, i);
    }

    for (int i = size - 1; i >= 0; i--) {
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;

        heapify(arr, i, 0);
    }
}

// Heapify function used in Heap Sort
void heapify(int arr[], int size, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < size && arr[left] > arr[largest]) {
        largest = left;
    }

    if (right < size && arr[right] > arr[largest]) {
        largest = right;
    }

    if (largest != i) {
        int temp = arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;

        heapify(arr, size, largest);
    }
}
