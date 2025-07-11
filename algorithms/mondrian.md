# Mondrian

Recursive algorithm to generate the style of Piet Mondrian (1872-1944), a Dutch painter known for his abstract geometric style.

## Algorithm

```{prf:algorithm} Mondrian
:label: mondrian-algorithm

**Inputs:** Rectangle

1. If the rectangle is too small:
    1. Return the rectangle
2. Else:
    1. Divide the rectangle into two smaller rectangles
    2. Recursively apply the Mondrian algorithm to each smaller rectangle
3. Return the combined rectangles
```

## Implementation

```python
import matplotlib.pyplot as plt
import numpy as np


class Rectangle:

    def __init__(self, x, y, width, height):
        self.x = x
        self.y = y
        self.width = width
        self.height = height

    def draw(self):
        # draw rectangle with random color with colormap
        colormap = plt.get_cmap("tab20")

        plt.fill(
            [self.x, self.x + self.width, self.x + self.width, self.x, self.x],
            [self.y, self.y, self.y + self.height, self.y + self.height, self.y],
            color=colormap(np.random.rand()),
        )

    def split(self):
        if np.random.rand() < 0.5:
            return self.split_horizontal()
        else:
            return self.split_vertical()

    def split_horizontal(self):
        split_height = np.random.uniform(0.3, 0.7) * self.height
        top = Rectangle(self.x, self.y, self.width, split_height)
        bottom = Rectangle(
            self.x, self.y + split_height, self.width, self.height - split_height
        )
        return top, bottom

    def split_vertical(self):
        split_width = np.random.uniform(0.3, 0.7) * self.width
        left = Rectangle(self.x, self.y, split_width, self.height)
        right = Rectangle(
            self.x + split_width, self.y, self.width - split_width, self.height
        )
        return left, right


def mondrian(x, y, width, height, min_size=0.3):

    # skip small rectangles
    if width < min_size or height < min_size:
        return

    # draw rectangle
    rect = Rectangle(x, y, width, height)
    rect.draw()

    # split rectangle
    if width > height:
        left, right = rect.split()
        mondrian(left.x, left.y, left.width, left.height)
        mondrian(right.x, right.y, right.width, right.height)
    else:
        top, bottom = rect.split()
        mondrian(top.x, top.y, top.width, top.height)
        mondrian(bottom.x, bottom.y, bottom.width, bottom.height)


if __name__ == "__main__":
    plt.figure(figsize=(8, 8))
    plt.axis("off")
    mondrian(0, 0, 1, 1)
    plt.show()
```

