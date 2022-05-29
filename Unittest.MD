## Structure of Python unittest

- Create test_file.py
- Import function, program etc which we want to test
- Import unittest
- Create test class
- Inside test class, create test function start with "test"
- Each test function use self.assert... to test

Below is an example to test a function plus(a,b)

```python
import unittest

def plus(a, b):
  return a + b

class TestPlus():
  def test_positive_number(self):
    result = plus(2, 3)
    self.assertEqual(result, 5)
  def test_negative_number(self):
    result = plus(-2, -3)
    self.assertEqual(result, -5)
 
unittest.main()
```

## Assert Methods:

### Equality and membership:
- Example: assertEqual, assertTrue, assertIn
- Full list: https://www.codecademy.com/courses/learn-intermediate-python-3/lessons/int-python-unit-testing/exercises/assert-methods-i-equality-and-membership

```python
import unittest
import entertainment

# Write your code below: 
class EntertainmentSystemTests(unittest.TestCase):

  def test_movie_license(self):
    daily_movie = entertainment.get_daily_movie()
    licensed_movies = entertainment.get_licensed_movies()
    self.assertIn(daily_movie, licensed_movies)


  def test_wifi_status(self):
    wifi_enabled = entertainment.get_wifi_status()
    self.assertTrue(wifi_enabled)


unittest.main()
```

### Quantitative methods:
- Example: asssertLess, assertAlmostEqual
- Full list: https://www.codecademy.com/courses/learn-intermediate-python-3/lessons/int-python-unit-testing/exercises/assert-methods-ii-quantitative-methods

```python
import unittest
import entertainment

class EntertainmentSystemTests(unittest.TestCase):

  def test_movie_license(self):
    daily_movie = entertainment.get_daily_movie()
    licensed_movies = entertainment.get_licensed_movies()
    self.assertIn(daily_movie, licensed_movies)

  def test_wifi_status(self):
    wifi_enabled = entertainment.get_wifi_status()
    self.assertTrue(wifi_enabled)

  # Write your code below:
  def test_maximum_display_brightness(self):
    brightness = entertainment.get_maximum_display_brightness()
    self.assertAlmostEqual(brightness, 400)

  def test_device_temperature(self):
    device_temp = entertainment.get_device_temp()
    self.assertLess(device_temp, 35)

unittest.main()
```

### Exception and Warning methods:
- Example: assertRaises, assertWarns
- Full list: https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertNotIsInstance

alerts.py
```python
import warnings

class PowerError(Exception):
    pass

class WaterLevelWarning(Warning):
    pass

def power_outage_detected(outage_detected):
    if outage_detected:
        raise PowerError('A power outage has been detected somewhere in the system')
    else:
        print('All systems receiving power')

def water_levels_check(liters):
    if liters < 200:
        warnings.warn('Water levels have fallen below 200 liters', WaterLevelWarning)
    else:
        print('Water levels are adequate')
        
unittest.main()
```

tests.py
```python
import unittest
import alerts

# Write your code here:
class SystemAlertTests(unittest.TestCase):
  def test_power_outage_alert(self):
    self.assertRaises(alerts.PowerError, alerts.power_outage_detected, True)

  def test_water_levels_warning(self):
    self.assertWarns(alerts.WaterLevelWarning, alerts.water_levels_check, 150)

unittest.main()
```

## Parameterizing Tests
- Python gives **test parameterization** to decrease repetition.
- subtest is used for this purpose

```python
import unittest
 
# The function we want to test
def times_ten(number):
    return number * 100
 
# Our test class
class TestTimesTen(unittest.TestCase):
 
    # A test method
    def test_times_ten(self):
        for num in [0, 1000000, -10]:
            with self.subTest(num):
                expected_result = num * 10
                message = 'Expected times_ten(' + str(num) + ') to return ' + str(expected_result)
                self.assertEqual(times_ten(num), expected_result, message)
                
unittest.main()
```

```python
import unittest
import entertainment

class EntertainmentSystemTests(unittest.TestCase):

  def test_movie_license(self):
    # Checkpoint 1
    daily_movies = entertainment.get_daily_movies()
    licensed_movies = entertainment.get_licensed_movies()

    # Checkpoint 2
    for movie in daily_movies:
      print(movie)
      # Checkpoint 3 & 4
      with self.subTest(movie):
        self.assertIn(movie, licensed_movies)

unittest.main()
```

