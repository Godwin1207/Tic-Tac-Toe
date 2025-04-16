#include <stdio.h>
#include <stdlib.h>

int num_of_zeroes(int n) {
    long long bin = 0;
    int rem, zeroes = 0, i = 1;
    while (n != 0) {
        rem = n % 2;
        if (rem == 0)
            zeroes++;
        n /= 2;
        bin += rem * i;
        i *= 10;
    }
    return zeroes;
}

typedef struct {
    int value;
    int zeroes;
} Number;

int compare(const void* a, const void* b) {
    Number* numA = (Number*)a;
    Number* numB = (Number*)b;
    
    if (numA->zeroes != numB->zeroes) {
        return numA->zeroes - numB->zeroes;
    }
    
    return numB->value - numA->value;
}

int main() {
    int n;
    printf("Jumlah angka: ");
    scanf("%d", &n);
    
    Number numbers[1000];
    
    printf("Input angka:\n");
    for (int i = 0; i < n; i++) {
        scanf("%d", &numbers[i].value);
        numbers[i].zeroes = num_of_zeroes(numbers[i].value);
    }
    
    qsort(numbers, n, sizeof(Number), compare);
    
    printf("[%d", numbers[0].value);
    int current_zeroes = numbers[0].zeroes;
    
    for (int i = 1; i < n; i++) {
        if (numbers[i].zeroes != current_zeroes) {
            printf("], [%d", numbers[i].value);
            current_zeroes = numbers[i].zeroes;
        } else {
            printf(" %d", numbers[i].value);
        }
    }
    printf("]\n");
    
    return 0;
}
