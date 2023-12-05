# Sorting Algorithm Visualizer with Pygame

## Overview

This project utilizes Pygame to create an interactive visualizer for sorting algorithms. Users can observe the dynamic sorting process of Heap Sort, Bubble Sort, and Insertion Sort.

## Screenshots

![Screenshot (21)](https://github.com/vjabhi000985/Sorting_Visualizer_Using_Pygame/assets/46738718/a31862b8-7ef8-434e-9317-a972769e5449)
Heap Sort in action

![Screenshot (19)](https://github.com/vjabhi000985/Sorting_Visualizer_Using_Pygame/assets/46738718/de244659-ab2d-4f0e-9d47-b446e671d92f)
Bubble Sort demonstration

![Screenshot (20)](https://github.com/vjabhi000985/Sorting_Visualizer_Using_Pygame/assets/46738718/70635dfd-068c-4a9e-9418-c6a417f1f887)
Insertion Sort visualization

## How to Use

1. Install Pygame: `pip install pygame`
2. Run the script: `python sorting_visualizer.py`
3. Select sorting algorithm and enjoy the visual representation.

## Code Snippets

### Initialize Pygame

```python
import pygame
pygame.init()
```

### Bubble Sort Code Snippet
```python
def bubble_sort(draw_attr, s_times, ascending=True):
	start = time.perf_counter()
	nums = draw_attr.nums

	for i in range(len(nums) - 1):
		for j in range(len(nums) - i - 1):
			num1 = nums[j]
			num2 = nums[j + 1]

			if (num1 > num2 and ascending) or (num1 < num2 and not ascending):
				nums[j], nums[j+1] = nums[j+1], nums[j]
				draw_attr.draw_list({j : draw_attr.GREEN, j + 1: draw_attr.RED},True)
				yield True

	s_times.bubble = round(time.perf_counter() - start, 2)
	draw_attr.draw_times(s_times)
```

### Insertion Sort Code Snippet
```python
def insertion_sort(draw_attr, s_times, ascending=True):
	start = time.perf_counter()
	nums = draw_attr.nums

	for i in range(1, len(nums)):
		curr = nums[i]

		while True:
			ascending_sort = i > 0 and nums[i-1] > curr and ascending
			descending_sort = i > 0 and nums[i-1] < curr and not ascending

			if not ascending_sort and not descending_sort:
				break

			nums[i] = nums[i - 1]
			i -= 1
			nums[i] = curr

			draw_attr.draw_list({i: draw_attr.GREEN, i - 1: draw_attr.RED}, True)
			yield True

	s_times.insertion = round(time.perf_counter() - start, 2)
	draw_attr.draw_times(s_times)
```

### Heap Sort Code Snippet
```python
def heapify(draw_attr, n, i, ascending):
    lst = draw_attr.nums

    curr = i
    left = 2 * i + 1
    right = 2 * i + 2

    if ascending:
        if left < n and lst[curr] < lst[left]:
            curr = left

        if right < n and lst[curr] < lst[right]:
            curr = right

    if not ascending:
        if left < n and lst[left] < lst[curr]:
            curr = left

        if right < n and lst[right] < lst[curr]:
            curr = right

    if curr != i:
        (lst[i], lst[curr]) = (lst[curr], lst[i])
        draw_attr.draw_list({i: draw_attr.GREEN, curr: draw_attr.RED}, True)
        heapify(draw_attr, n, curr, ascending)


def heap_sort(draw_attr, s_times, ascending=True):
    start = time.perf_counter()
    lst = draw_attr.nums

    n = len(lst)
    for i in range(n // 2 - 1, -1, -1):
        heapify(draw_attr, n, i, ascending)

    for i in range(n - 1, 0, -1):
        (lst[i], lst[0]) = (lst[0], lst[i])
        draw_attr.draw_list({i: draw_attr.GREEN, 0: draw_attr.RED}, True)
        heapify(draw_attr, i, 0, ascending)
        yield True

    s_times.heap = round(time.perf_counter() - start, 2)
    draw_attr.draw_times(s_times)
```

## Credits
Developed by *Pandey Abhishek Nath Roy*
