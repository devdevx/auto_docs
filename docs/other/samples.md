# Samples

## Code

````py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i): # (1)
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
````

1.  I'm a code annotation! I can contain `code`, __formatted    text__, images, ... basically anything that can be written in Markdown.

Other thing.