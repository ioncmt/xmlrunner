# xmlrunner

A unittest test runner that can save test results to XML files adhering to the JUnit Report
Structure and therefore can be consumed by a wide range of tools, such as build systems, IDEs,
continuous integration servers and Confluence.

If you find a bug the best way to have it fixed is to fix it yourself and to make a pull request.


## Features

- Writes the whole report into a single XML file
- Flattens the structure to contain only one test suite (to achieve compatibility with the standard
Confluence JUnit Report Macro)
- Removes `'` and `"` from the report file (to achieve compatibility with the standard Confluence
JUnit Report Macro)
- Pipes `print()` output to the commandline _and_ the report file


## Requirements

- Python 3.5+


## Installation

To get the latest version: Clone this repository and then run

````bash
$ cd xmlrunner
$ sudo python setup.py install
````

## Usage

Write the rest of your Testing Setup as usual using python's unittest.

Then finish it up with a code block like in the following example:

````python
date_formatted = datetime.datetime.now().strftime('%Y-%d-%m_%H-%M-%S')

path_to_xml = os.path.abspath(os.path.join(
    os.path.dirname(__file__),
    '_reports/report_%s.xml'%(date_formatted)
))
os.makedirs(os.path.dirname(path_to_xml), exist_ok=True)

with open(path_to_xml, 'w') as file_output:
    xml_runner = xmlrunner.XMLTestRunner(
        output=file_output
    )
    result = xml_runner.run(main_test_suite)
````
