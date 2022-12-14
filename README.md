# pytest
### installation
- pip install pytest
### using in py files
- import pytest
### run all tests with pytest
- pytest tests/ 
- where tests is a folder contains all test classes with starts or ends with test in name

### grouping in tests
- mark it in tests
@pytest.mark.<markername>
- then run using -m flag
pytest tests/ -m "sanitytests"

### calling pytests through python
python -m pytest -q test_sample.py  

### run tests with specific keyword in test method name
pytest tests/ -k "metric"

### stop test run on first failure or max failure

pytest tests/ -x
pytest tests/ --maxfail=2

### retry failures
pip install pytest-rerunfailures
pytest tests/ --reruns 5

### disable test
@pytest.mark.skip(reason="no way of currently testing this")

### multithreading
pip install pytest-xdist
pytest tests/ -n 3

### ordering
@pytest.mark.run(order=17)

### using cmd parameters in pytest
- supply param from cmd
pytest tests\ --env qa

- read from cmd in conftest file
def pytest_addoption(parser):
    parser.addoption("--env", action="store", default="environment value is not provided")

def pytest_sessionstart(session):
    env_param = session.config.getoption("--env")

- set and get param using os.getenv
os.environ['env'] = env_param
os.getenv['env']

### fixtures/beforetest

- create fixture in conftest
@pytest.fixture
def input_value():
   input = 10
   return input

- use it in tests
def test_divisible_by_3(input_value):
   assert input_value % 3 == 0

### data parameterization 

@pytest.mark.parametrize("num, output",[(1,11),(2,22),(3,35),(4,44)])
def test_multiplication_11(num, output):
   assert 11*num == output

### reporting in pytest
--pytest default html
--pytest-html-reporter
--junit
pytest tests --junitxml="result.xml"

--allure
pytest tests --alluredir=/allure
allure serve allure