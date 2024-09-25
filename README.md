//DSA assignment 2
//question 1
#include <stdio.h>
#include <stdlib.h>

// Function to allocate memory dynamically for a matrix
int** allocateMatrix(int rows, int cols) {
int** matrix = (int**)malloc(rows * sizeof(int*));
for (int i = 0; i < rows; i++) {
matrix[i] = (int*)malloc(cols * sizeof(int));
}
return matrix;
}

// Function to input a matrix
void inputMatrix(int** matrix, int rows, int cols) {
printf("Enter the elements of the matrix (%d x %d):\n", rows, cols);
for (int i = 0; i < rows; i++) {
for (int j = 0; j < cols; j++) {
scanf("%d", &matrix[i][j]);
}
}
}

// Function to multiply two matrices
int** multiplyMatrices(int** mat1, int** mat2, int r1, int c1, int c2) {
// Allocate memory for the result matrix
int** result = allocateMatrix(r1, c2);

// Perform matrix multiplication

for (int i = 0; i < r1; i++) {
for (int j = 0; j < c2; j++) {
result[i][j] = 0;
for (int k = 0; k < c1; k++) {
result[i][j] += mat1[i][k] * mat2[k][j];
}
}
}

return result;
}

// Function to display a matrix
void displayMatrix(int** matrix, int rows, int cols) {
printf("Matrix (%d x %d):\n", rows, cols);
for (int i = 0; i < rows; i++) {
for (int j = 0; j < cols; j++) {
printf("%d ", matrix[i][j]);
}
printf("\n");
}
}

// Free the dynamically allocated memory for a matrix
void freeMatrix(int** matrix, int rows) {
for (int i = 0; i < rows; i++) {
free(matrix[i]);
}
free(matrix);
}

int main() {
int r1, c1, r2, c2;

// Input dimensions of the matrices
printf("Enter the number of rows and columns for the first matrix: ");
scanf("%d %d", &r1, &c1);

printf("Enter the number of rows and columns for the second matrix: ");
scanf("%d %d", &r2, &c2);

// Check if multiplication is possible
if (c1 != r2) {
printf("Matrix multiplication not possible with these dimensions.\n");
return -1;
}

// Allocate memory for both matrices
int** mat1 = allocateMatrix(r1, c1);
int** mat2 = allocateMatrix(r2, c2);

// Input matrices
inputMatrix(mat1, r1, c1);
inputMatrix(mat2, r2, c2);

// Multiply matrices
int** result = multiplyMatrices(mat1, mat2, r1, c1, c2);

// Display the result
displayMatrix(result, r1, c2);

// Free allocated memory
freeMatrix(mat1, r1);
freeMatrix(mat2, r2);
freeMatrix(result, r1);

return 0;
}
