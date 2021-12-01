# Problems
- find whether a point is inside or outside a polygon ([pseudocode](#odd-even-rule))
  - idea
    - a line from point in/on the polygon would intersect it odd no of times
    - for point outside it would intersect even no of times


# pseudocodes
## odd even rule
```py
def isInside(point, polygon, Nvertices):
  # if Nvertices < 3 return;
  extreme = Point(point.y, INF)
  count = i = 0
  while True:
    next = (i+1)%Nvertices

    if intersecting_line_segement(point, extreme, polygon[i], polygon[next]):

    # case to handle when point is on polygon
      if colinear(polygon[i],point, polygon[next]):
        return on_line_segment(polygon[i], p, polygon[next])  # return true or false

        count++
    if i == 0:
      break

  # odd count indicates point inside
  return count%2 == 1
```