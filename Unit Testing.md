# Why pyTest
* Run standalone test function as it's own case.
* Easy to read syntax, using standard `assert` method.
* Powerful CLI
* Automates test setup, teardown, and common test scenarios.
* Great to use with CI tools like Travis, Jenkins and Circle CI
* Actively maintained with open source community.

Follow GitHub link for files. Switch branches to see end state.

# Test Driven Development (TDD)
1. Write a test that will fail as there's no code.
2. Write just enough code to pass the test.
3. Refactor as necessary untilall tests pass.

# Basic Tests and Assertions
Exercise Files:
* scripts/chp2/video2/mapmaker_start.py
* tests/chp2/video2/test_mapmaker_start.py

### Running pytest
`pytest -k map` - The 'k' flag will only run test files with "map" in the name.

test function:
```
def test_make_one_point():
    p1 = Point()
```

Will fail. Add:
```
from scripts.chp2.video2.mapkamker_start import Point
```

Will pass, but pyflakes will fail for unused variable:
```
from scripts.chp2.video2.mapkamker_start import Point


def test_make_one_point():
    p1 = Point("Dakar", 14.7167, 17.467)
    assert p1.get_lat_long() ==  (14.7167, 17,4677)

```

Will fail. Now updated Point class:
```
class Point():
    def __init__(self, city_name, lat, long):
        seld.city_name = city_name
        self.lat = lat
        self.long = long

    def get_lat_long(self):
        return (self.lat, self.long)

```

### Exceptions
You can make pytest check for an exception by writing a test like:
File `test_exceptions_start.py`
```
def  test_invalid_point_generation():
    with pytest.raises(Exception) as exp:
        raise(Exception)
```
If an exception is raised (as  with  our code) the test will not fail. If it is not, the test will fail when it is raised.
```
def  test_invalid_point_generation():
    with pytest.raises(Exception) as exp:
        Point("Buenos Aires", 12.11386, -555.08269)
```

Run with `pytest -k except`

Update Point:
```
class Point():
    def __init__(self, city_name, lat, long):
        seld.city_name = city_name

        if not (-90 <= lat  <= 90) or (-180 <= long <= 180):
            raise ValueError("Invalid lat or long")

        self.lat = lat
        self.long = long

    def get_lat_long(self):
        return (self.lat, self.long)

```

```
def  test_invalid_point_generation():
    with pytest.raises(Exception) as exp:
        Point("Buenos Aires", 12.11386, -555.08269)

    assert str(exp.value) == "Invalid lat or long")
```

### Debugging
Start debugging:
```breakpoint()```
Inspect variables available:
```{k: v for k, v in locals().items() if '__' not in k and 'pdb' not in k}```

# Happy Path Testing
* Shows how system should work with correct data.
* Organise positive cases into their own functions.

# Sad Path  Testing
*  Show how your system validates or raises errors with invalid inputs.