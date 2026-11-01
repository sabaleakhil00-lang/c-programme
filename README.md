#include <stdio.h>

#define MAX 100

// Function for Linear Search
int linearSearch(int a[], int n, int key)
{
    int i;

    for (i = 0; i < n; i++)
    {
        if (a[i] == key)
            return i;
    }

    return -1;
}

// Function for Binary Search
int binarySearch(int a[], int n, int key)
{
    int low = 0, high = n - 1, mid;

    while (low <= high)
    {
        mid = (low + high) / 2;

        if (a[mid] == key)
            return mid;
        else if (a[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }

    return -1;
}

int main()
{
    int a[MAX], n, i, choice, key, result;

    printf("Enter number of students: ");
    scanf("%d", &n);

    if (n <= 0 || n > MAX)
    {
        printf("Invalid number of students!\n");
        return 1;
    }

    printf("Enter roll numbers in random order:\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }

    do
    {
        printf("\n===== MENU =====\n");
        printf("1. Linear Search\n");
        printf("2. Binary Search\n");
        printf("3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                printf("Enter roll number to search: ");
                scanf("%d", &key);

                result = linearSearch(a, n, key);

                if (result != -1)
                    printf("Student attended the training program.\n");
                else
                    printf("Student did not attend the training program.\n");

                break;

            case 2:
                // Sort the array before Binary Search
                for (i = 0; i < n - 1; i++)
                {
                    int j;
                    for (j = 0; j < n - i - 1; j++)
                    {
                        if (a[j] > a[j + 1])
                        {
                            int temp = a[j];
                            a[j] = a[j + 1];
                            a[j + 1] = temp;
                        }
                    }
                }

                printf("Sorted roll numbers: ");
                for (i = 0; i < n; i++)
                    printf("%d ", a[i]);

                printf("\nEnter roll number to search: ");
                scanf("%d", &key);

                result = binarySearch(a, n, key);

                if (result != -1)
                    printf("Student attended the training program.\n");
                else
                    printf("Student did not attend the training program.\n");

                break;

            case 3:
                printf("Exiting program...\n");
                break;

            default:
                printf("Invalid choice! Please try again.\n");
        }

    } while (choice != 3);

    return 0;
}
