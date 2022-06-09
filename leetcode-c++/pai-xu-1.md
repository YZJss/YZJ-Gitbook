# 排序(1)

### 冒泡排序

```
void bubblesort(vector<int> &nums) {
    for (int i = 0; i < nums.size(); ++i) {
        for (int j = 0; j < nums.size() - 1 - i; ++j) {
            if (nums[j] > nums[j + 1]) {
                swap(nums[j], nums[j + 1]);
            }
        }
    }
}
```

### 选择排序

```
void selectsort(vector<int> &nums) {
    for (int i = 0; i < nums.size() - 1; ++i) {
        int min_index = i;
        for (int j = i + 1; j < nums.size(); ++j) {
            if (nums[j] < nums[min_index]) {
                min_index = j;
            }
        }
        if (min_index != i) {
            swap(nums[min_index], nums[i]);
        }
    }
}
```

### 插入排序

```
void insertsort(vector<int> &num) {
    for (int i = 1; i < num.size(); i++) {
        int insert_num = num[i], j;
        for (j = i - 1; j >= 0; j--) {
            if (num[j] > insert_num)
                num[j + 1] = num[j];
            else
                break;
        }
        num[j + 1] = insert_num;
    }
}
```

### 快速排序

```
int partition(vector<int> &arr, int low, int high) {
    int pivot = arr[high];  
    int i = (low - 1);      
    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++;
            swap(arr[j], arr[i]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (i + 1);
}

void quicksort(vector<int> &arr, int low, int high) {
    if (low < high) {
        int p = partition(arr, low, high);
        quicksort(arr, low, p - 1);
        quicksort(arr, p + 1, high);
    }
}
```

### 堆排序

```
void heapify(vector<int> &nums, int n, int i) {
    if (i >= n) {
        return;
    }
    int c1 = 2 * i + 1; //子节点 c1 c2
    int c2 = 2 * i + 2;
    int max = i;    // 父节点  max
    if (c1 < n && nums[c1] > nums[max]) {
        max = c1;
    }
    if (c2 < n && nums[c2] > nums[max]) {
        max = c2;
    }
    if (max != i) {
        swap(nums[max], nums[i]);
        heapify(nums, n, max);
    }
}

void build_heap(vector<int> &nums, int n) {
    int last_node = n - 1;
    int parent = (last_node - 1) / 2;
    for (int i = parent; i >= 0; --i) {
        heapify(nums, n, i);
    }
}

void heap_sort(vector<int> &nums, int n) {
    build_heap(nums, n);
    for (int i = n - 1; i >= 0; i--) {
        swap(nums[i], nums[0]);
        heapify(nums, i, 0);
    }
}
```

### 归并排序

```
vector<int> merge(vector<int> left, vector<int> right) {
    vector<int> res;
    int i = 0, j = 0;
    while (i < left.size() && j < right.size()) {
        if (left[i] <= right[j])
            res.push_back(left[i++]);
        else
            res.push_back(right[j++]);
    }
    if (i == left.size())
        res.insert(res.end(), right.begin() + j, right.end());
    else if (j == right.size())
        res.insert(res.end(), left.begin() + i, left.end());
    return res;
}

vector<int> mergeSort(vector<int>& arr) {
    if (arr.size() < 2) return arr;
    int mid = arr.size() / 2;
    vector<int> left(arr.begin(), arr.begin() + mid);
    vector<int> right(arr.begin() + mid, arr.end());
    return merge(mergeSort(left), mergeSort(right));
}
```

![img](https://cdn.jsdelivr.net/gh/YZJss/tuchuang@main/0.jpeg)

```
#include "vector"

using namespace std;

void print(vector<int> &nums) {
    for (int i = 0; i < nums.size(); ++i) {
        printf("%d ", nums[i]);
    }
    printf("\n");
}
int main() {
    vector<int> num = {3, 1, 5, 8, 6, 2, 0, 9, 4, 7};
    print(num);
    //quicksort(num, 0, 9);
    //selectsort(num);
    //bubblesort(num);
    //insertsort(num);
    //heap_sort(num, 10);
    vector<int> b = mergeSort(num);
    print(b);
    return 0;
}
```
