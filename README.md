# algoritmos-3

## 1. Problema
2

3
### Encontrar la cantidad de inversiones en una matriz  (Usando Merge Sort)
4

5
La cantidad de inversiones de una matriz indica: qué tan lejos (o cerca) está la matriz de ser ordenada. Si el conjunto ya está ordenado, el recuento de inversión es 0. Si el conjunto se ordena en orden inverso, el recuento de inversión es el máximo.
6

7
De manera más clara, dos elementos a [i] y a [j] forman una inversión si a [i]> a [j] e i <j
8

9
### Ejemplo:
10

11
La secuencia 2, 4, 1, 3, 5 tiene tres inversiones (2, 1), (4, 1), (4, 3).
12

13
### Usar como ejemplo el vector {1, 20, 6, 4, 5}

habrian 3 inversiones
{20,6}
{6,4}
{6,5}

 parte del codigo en java;
 
 
long merge(int[] arr, int[] left, int[] right) {
    int i = 0, j = 0, count = 0;
    while (i < left.length || j < right.length) {
        if (i == left.length) {
            arr[i+j] = right[j];
            j++;
        } else if (j == right.length) {
            arr[i+j] = left[i];
            i++;
        } else if (left[i] <= right[j]) {
            arr[i+j] = left[i];
            i++;                
        } else {
            arr[i+j] = right[j];
            count += left.length-i;
            j++;
        }
    }
    return count;
}

long invCount(int[] arr) {
    if (arr.length < 2)
        return 0;

    int m = (arr.length + 1) / 2;
    int left[] = Arrays.copyOfRange(arr, 0, m);
    int right[] = Arrays.copyOfRange(arr, m, arr.length);

    return invCount(left) + invCount(right) + merge(arr, left, right);
}
