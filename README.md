## Gambaran Umum

Kode ini berfungsi untuk menggabungkan array menggunakan konsep Parallel Merge dalam Komputasi Paralel.

## Bahasa Pemrograman

Kode proyek ini ditulis menggunakan bahasa pemrograman Python.

## Software Pendukung

Proyek ini dikembangkan menggunakan [Visual Studio Code](https://code.visualstudio.com/download).

## Cara Penggunaan

1. Buka proyek menggunakan Visual Studio Code.
2. Kemudian Run Code untuk menampilkan hasil array.

## Contoh Penggunaan Program

```py
import concurrent.futures

def parallel_merge(arr1, arr2):
    result = [0] * (len(arr1) + len(arr2))
    i = j = k = 0

    with concurrent.futures.ThreadPoolExecutor() as executor:
        futures = []
        while i < len(arr1) and j < len(arr2):
            if arr1[i] < arr2[j]:
                futures.append(executor.submit(copy_value, arr1[i], result, k))
                i += 1
            else:
                futures.append(executor.submit(copy_value, arr2[j], result, k))
                j += 1
            k += 1

        while i < len(arr1):
            futures.append(executor.submit(copy_value, arr1[i], result, k))
            i += 1
            k += 1

        while j < len(arr2):
            futures.append(executor.submit(copy_value, arr2[j], result, k))
            j += 1
            k += 1

    # Wait for all futures to complete
    concurrent.futures.wait(futures)

    return result

def copy_value(value, result, index):
    result[index] = value

# Contoh penggunaan
arr1 = [1, 3, 5, 7]
arr2 = [2, 4, 6, 8]

result = parallel_merge(arr1, arr2)
print("\nHasil Merge:", result)
