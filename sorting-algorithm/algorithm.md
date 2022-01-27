# Sorting Algorithms

## Insertion

### Ascending

```c
for (int i = 0; i < ARRAY_LENGTH; i++) {
        int j = i + 1;
        while (j < ARRAY_LENGTH) {
            if (*(sommes + i) > *(sommes + j)) {
                int tmp = *(sommes + i);
                *(sommes + i) = *(sommes + j);
                *(sommes + j) = tmp;
                j = i;
            }
            j++;
        }
    }
```

### Descending

```c
for (int i = 0; i < ARRAY_LENGTH; i++) {
        int j = i + 1;
        while (j < ARRAY_LENGTH) {
            if (*(sommes + i) < *(sommes + j)) {
                int tmp = *(sommes + i);
                *(sommes + i) = *(sommes + j);
                *(sommes + j) = tmp;
                j = i;
            }
            j++;
        }
    }
```