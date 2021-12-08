# Model constraints
- SQL has a *check* integrity constraint apart from *not null*, *unique* and *references*
- django provides addition of this constraint using the `CheckConstraint` class, by specifying the `constraints` property in a Model's Meta class.
```python
class model(models.Model):
  class Meta:
    constraints = models.CheckConstraint(
      name=...,
      check=models.Q()
    )
```