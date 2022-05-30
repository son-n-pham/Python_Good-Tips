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

## Test Fixtures

One of the most important principles of testing is that tests need to occur in a known state. If the conditions in which a test runs are not controlled, then our results could contain false negatives (invalid failed results) or false positives (invalid passed results).

This is where test fixtures come in. A test fixture is a mechanism for ensuring proper test setup (putting tests into a known state) and test teardown (restoring the state prior to the test running). Test fixtures guarantee that our tests are running in predictable conditions, and thus the results are reliable.

The unittest framework automatically identifies setup and teardown methods based on their names. A method named setUp runs before each test case in the class. Similarly, a method named tearDown gets called after each test case.

TEST file
```python
def power_cycle_device():
  print('Power cycling bluetooth device...')
 
class BluetoothDeviceTests(unittest.TestCase):
  def setUp(self):
    power_cycle_device()
 
  def test_feature_a(self):
    print('Testing Feature A')
 
  def test_feature_b(self):
    print('Testing Feature B')
 
  def tearDown(self):
    power_cycle_device()

unittest.main()
```

RESULT
```
Power cycling bluetooth device...
Testing Feature A
Power cycling bluetooth device...
.Power cycling bluetooth device...
Testing Feature B
Power cycling bluetooth device...
.
----------------------------------------------------------------------
Ran 2 tests in 0.000s
 
OK
```


TEST file
```python
def power_cycle_device():
    print('Power cycling bluetooth device...')
 
class BluetoothDeviceTests(unittest.TestCase):
  @classmethod
  def setUpClass(cls):
    power_cycle_device()
 
  def test_feature_a(self):
    print('Testing Feature A')
 
  def test_feature_b(self):
    print('Testing Feature B')
 
  @classmethod
  def tearDownClass(cls):
    power_cycle_device()

unittest.main()
```

RESULT
```
Power cycling bluetooth device...
Testing Feature A
Testing Feature B
Power cycling bluetooth device...
 
----------------------------------------------------------------------
Ran 2 tests in 0.000s
 
OK
```


kiosk.py
```python
def power_on_kiosk():
    print('Powering on the check-in kiosk...')


def return_to_welcome_page():
    print('Returning check-in kiosk to Welcome Page')


def power_off_kiosk():
    print('Powering off the check-in kiosk...')
```

tests.py
```python
import unittest
import kiosk

class CheckInKioskTests(unittest.TestCase):

  def test_check_in_with_flight_number(self):
    print('Testing the check-in process based on flight number')

  def test_check_in_with_passport(self):
    print('Testing the check-in process based on passport')

  # Write your code below:
  @classmethod
  def setUpClass(cls):
    kiosk.power_on_kiosk()
    

  @classmethod
  def tearDownClass(cls):
    kiosk.power_off_kiosk()

  def setUp(self):
    kiosk.return_to_welcome_page()

unittest.main()
```

RESULT
```
Powering on the check-in kiosk...
Returning check-in kiosk to Welcome Page
Testing the check-in process based on flight number
Returning check-in kiosk to Welcome Page
Testing the check-in process based on passport
Powering off the check-in kiosk...
..
----------------------------------------------------------------------
Ran 2 tests in 0.000s

OK
```

## Skip test

Sometimes we have tests that should only run in a particular context. For example, we might have a group of tests that only runs on the Windows operating system but not Linux or macOS. For these situations, it’s helpful to be able to skip tests.

The unittest framework provides two different ways to skip tests:
- The @unittest skip decorator


```python
import sys
 
class LinuxTests(unittest.TestCase):
 
    @unittest.skipUnless(sys.platform.startswith("linux"), "This test only runs on Linux")
    def test_linux_feature(self):
        print("This test should only run on Linux")
 
    @unittest.skipIf(not sys.platform.startswith("linux"), "This test only runs on Linux")
    def test_other_linux_feature(self):
        print("This test should only run on Linux")
```

- The skipTest() method
 
```python
import sys
 
class LinuxTests(unittest.TestCase):
 
    def test_linux_feature(self):
        if not sys.platform.startswith("linux"):
            self.skipTest("Test only runs on Linux")
```

Both give the same result. Below is the result if the test was run on macOS

```
s
----------------------------------------------------------------------
Ran 1 test in 0.000s
 
OK (skipped=1)
```

More example

entertainment.py
```python
def regional_jet():
    print('This is a regional jet...')
    return True

def get_daily_movie():
    print('Retrieving the movie set to play on today\'s flight...')
    return 'Parasite'


def get_licensed_movies():
    print('Retrieving the list of licenses movies from the database...')
    licensed_movies = ['Parasite', 'Nomadland', 'Roma']
    return licensed_movies


def get_wifi_status():
    print('Checking WiFi signal...')
    print('WiFi is active')
    return True

def get_device_temp():
    print('Reading the temperature of the entertainment system device...')
    return 33.2

def get_maximum_display_brightness():
    print('Calculating maximum display brightness in nits...')
    return 399.99999999
```

tests.py
```python
import unittest
import entertainment

class EntertainmentSystemTests(unittest.TestCase):
  # Checkpoint 1
  @unittest.skipIf(entertainment.regional_jet(), 'Not available on regional jets')
  def test_movie_license(self):
    daily_movie = entertainment.get_daily_movie()
    licensed_movies = entertainment.get_licensed_movies()
    self.assertIn(daily_movie, licensed_movies)

  # Checkpoint 2
  @unittest.skipUnless(entertainment.regional_jet() is False, 'Not available on regional jets')
  def test_wifi_status(self):
    wifi_enabled = entertainment.get_wifi_status()
    self.assertTrue(wifi_enabled)

  # Checkpoint 3
  def test_device_temperature(self):
    if entertainment.regional_jet():
      self.skipTest('Not available on regional jets')
    device_temp = entertainment.get_device_temp()
    self.assertLess(device_temp, 35)

  # Checkpoint 3
  def test_maximum_display_brightness(self):
    if entertainment.regional_jet():
      self.skipTest('Not available on regional jets')
    brightness = entertainment.get_maximum_display_brightness()
    self.assertAlmostEqual(brightness, 400)


unittest.main()
```

RESULT
```
This is a regional jet...
This is a regional jet...
This is a regional jet...
This is a regional jet...
ssss
----------------------------------------------------------------------
Ran 4 tests in 0.000s

OK (skipped=4)
```

## Expected Failures
- Sometimes we have a test that we know will fail. This could happen when a feature has a known bug or is designed to fail on purpose. 
- In this case, we wouldn’t want an expected failure to cloud our test results. Rather than simply skipping the test, unittest provides a way to mark tests as expected failures. 
- Expected failures are counted as passed in our test results. If the test passes when we expected it to fail, then it is marked as failed in test results.
- To setup a test to have an expected failure, we can use the expectedFailure decorator.

```python
class FeatureTests(unittest.TestCase):
 
    @unittest.expectedFailure
    def test_broken_feature(self):
        raise Exception("This test is going to fail")
```

RESULT: No failure in test result as failure is expected

```
x
----------------------------------------------------------------------
Ran 1 test in 0.000s
 
OK (expected failures=1)
```

### More example

feedback.py

```python
class FormError(Exception):
    pass

def issue_survey():
    print('Opening customer survey')
    raise FormError('An error occurred when opening customer survey form!')

def log_customer_complaint():
    print('Opening customer complaint form')
    print('Logged customer complaint')
    return 'Success'
```
