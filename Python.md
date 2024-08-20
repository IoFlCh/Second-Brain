# try:
```python
def main():
	x = get_int()
	print(f"x is {x}")

def get_int():
	while True:
		try:
			return int(input("What's x?"))
		except ValueError:
			print("x is not an integer")

main()
```
```python
def main():
	x = get_int()
	print(f"x is {x}")

def get_int():
	while True:
		try:
			return int(input("What's x?"))
		except ValueError:
			pass

main()
```
```python
def main():
	x = get_int("What's x? ")
	print(f"x is {x}")

def get_int(prompt):
	while True:
		try:
			return int(input(prompt))
		except ValueError:
			pass

main()
```
# Random:
```python
import random

coin = random.choice(["heads", "tails"])
print(coin)
```
```python
import random

number = random.randint(1, 10)
print(number)
```
```python
import random

cards = ["jack", "queen", "king"]
random.shuffle(cards)
for card in cards:
	print(card)
```
# Statistics:
```python
import statistics

print(statistics.mean([100, 90]))
```
# match:
```python
  name = input("What's your name? ")

  match name: 
	  case "Harry":
		  print("Gryffindor")
	  case "Hermione":
		  print("Gryffindor")
	  case "Ron": 
		  print("Gryffindor")
	  case "Draco":
		  print("Slytherin")
	  case _:
		  print("Who?")
```
# Dictionaries:
```python
students = [
	{"name": "Hermoine", "house": "Gryffindor", "patronus": "Otter"},
	{"name": "Harry", "house": "Gryffindor", "patronus": "Stag"},
	{"name": "Ron", "house": "Gryffindor", "patronus": "Jack Russell terrier"},
	{"name": "Draco", "house": "Slytherin", "patronus": None},
]

for student in students:
	print(student["name"], student["house"], student["patronus"], sep=", ")
```
# Command line arguments:
```python
python average.py 100 90

import sys

if len(sys.argv) < 2:
	sys.exit("Too few arguments")
elif len(sys.argv) > 2:
	sys.exit("Too many arguments")
else:
	print((sys.argv[0] + sys.argv[1])/2)
print("hello, my name is", sys.argv[1])
```
# Packages:
```python
import cowsay
import sys

if len(sys.argv) == 2:
	cowsay.cow("hello, " + sys.argv[1])
```
# APIs:
```python
python itunes.py weezer

import requests
import sys

if len(sys.argv) != 2:
	sys.exit()

response = requests.get("https://itunes.apple.com/search?entity=song&limit=1&term=" + sys.argv[1])
print(response.json())
```
```python
import json
import requests
import sys

if len(sys.argv) != 2:
	sys.exit()

response = requests.get("https://itunes.apple.com/search?entity=song&limit=1&term=" + sys.argv[1])
print(json.dumps(response.json(), indent=2))
```
```python
import json
import requests
import sys

if len(sys.argv) != 2:
	sys.exit()

response = requests.get("https://itunes.apple.com/search?entity=song&limit=50&term=" + sys.argv[1])

o = response.json()
for result in o["results"]:
	print(result["trackName"])
```
# assert:
```python
def test_square():
	assert square(2) == 4
	assert square(3) == 9
```
```python
def test_square():
	try:
		assert square(2) == 4
	except AssertionError:
		print("2 squared is not 4")
	try:
		assert square(3) == 9
	except AssertionError:
		print("3 squared is not 9")
	try:
		assert square(-2) == 4
	except AssertionError:
		print("-2 squared is not 4")
	try:
		assert square(-3) == 9
	except AssertionError:
		print("-3 squared is not 9")
	try:
		assert square(0) == 0
	except AssertionError:
		print("0 squared is not 0")
```
# I/O:
```python
names = []

for _ in range(3):
	names.append(input("What's your name?" ))

for name in sorted(names):
	print(f"hello, {name}")
```
# open:
```python
name = input("What's your name? ")

file = open("names.txt", "a")
file.write(f"{name}\n")
file.close()
```
# with:
```python
name = input("What's your name? ")

with open("names.txt", "a") as file:
	file.write(f"{name}\n")
```
```python
names = []

with open("names.txt") as file:
	for line in file:
		names.append(line.rstrip())

for name in sorted(names):
	print(f"hello, {name}")
```
# CSV:
```CSV
Hermoine,Gryffindor
Harry,Gryffindor
Ron,Gryffindor
Draco,Slytherin
```

```python
with open("students.csv") as file:
	for line in file:
		row = line.rstrip().split(",")
		print(f"{row[0]} is in {row[1]}")
```

```python
with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		print(f"{name} is in {house}")
```

```python
students = []

with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		student = {}
		student["name"] = name
		student["house"] = house
		students.append(student)

for student in students:
	print(f"{student['name']} is in {student['house']}")
```

```python
students = []

with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		student = {"name": name, "house": house}
		students.append(student)

for student in students:
	print(f"{student['name']} is in {student['house']}")
```

```python
students = []

with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		students.append({"name": name, "house": house})


def get_name(student):
	return student["name"]


for student in sorted(students, key=get_name):
	print(f"{student['name']} is in {student['house']}")
```

```python
students = []

with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		students.append({"name": name, "house": house})

for student in sorted(students, key=lambda student: student["name"]):
	print(f"{student['name']} is in {student['house']}")
```

```CSV
Harry,"Number Four, Privet Drive"
Ron,The Burrow
Draco,Malfoy Manor
```

```python
import csv

students = []

with open("students.csv") as file:
	reader = csv.reader(file)
	for row in reader:
		students.append({"name": row[0], "home": row[1]})

for student in sorted(students, key=lambda student: student["name"]):
	print(f"{student['name']} is from {student['home']}")
```

```CSV
name,home
Harry,"Number Four, Privet Drive"
Ron,The Burrow
Draco,Malfoy Manor
```

```python
import csv

students = []

with open("students.csv") as file:
	reader = csv.DictReader(file)
	for row in reader:
		students.append({"name": row["name"], "home": row["home"]})

for student in sorted(students, key=lambda student: student["name"]):
	print(f"{student['name']} is in {student['home']}")
```

```python
import csv

name = input("What's your name? ")
home = input("Where's your home? ")

with open("students.csv", "a") as file:
	writer = csv.DictWriter(file, fieldnames=["name", "home"])
	writer.writerow({"name": name, "home": home})
```
# Binary Files and PIL:
```python
import sys

from PIL import Image

images = []

for arg in sys.argv[1:]:
	image = Image.open(arg)
	images.append(image)

images[0].save(
	"costumes.gif", save_all=True, append_images=[images[1]], duration=200, loop=0
)
```
# Regular Expressions:
`re.search(pattern, string, flags=0)`
```python
.   any character except a new line
*   0 or more repetitions
+   1 or more repetitions
?   0 or 1 repetition
{m} m repetitions
{m,n} m-n repetitions

if re.search(".+@.+", email):
if re.search(r".+@.+\.edu", email):

^   matches the start of the string
$   matches the end of the string or just before the newline at the end of the string

if re.search(r"^.+@.+\.edu$", email):

[]    set of characters
[^]   complementing the set

if re.search(r"^[^@]+@[^@]+\.edu$", email):
# [^@] - any character at the beginning, except "@"

if re.search(r"^[a-zA-Z0-9_]+@[a-zA-Z0-9_]+\.edu$", email):
# characters must be between `a` and `z`, between `A` and `Z`, between `0` and `9` and potentially include an `_` symbol
if re.search(r"^\w+@\w+\.edu$", email):
# \w is the same as [a-zA-Z0-9_]

d    decimal digit
\D    not a decimal digit
\s    whitespace characters
\S    not a whitespace character
\w    word character, as well as numbers and the underscore
\W    not a word character

if re.search(r"^\w+@\w.+\.(com|edu|gov|net|org)$", email):

re.IGNORECASE
re.MULTILINE
re.DOTALL
if re.search(r"^\w+@\w+\.edu$", email, re.IGNORECASE):

A|B     either A or B
(...)   a group
(?:...) non-caputuring version
if re.search(r"^\w+@(\w+\.)?\w+\.edu$", email, re.IGNORECASE):
#both malan@cs50.harvard.edu and malan@harvard.edu are considered valid

^[a-zA-Z0-9.!#$%&'*+\/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$

  
```
- Placing an `r` in front of a string tells the Python interpreter to treat the string as a raw string, similar to how placing an `f` in front of a string tells the Python interpreter to treat the string as a format string
# Cleaning user input:
```python
import re

name = input("What's your name? ").strip()
matches = re.search(r"^(.+), (.+)$", name)
if matches:
	last, first = matches.groups()
	name = first + " " + last
print(f"hello, {name}")
```
```python
import re

name = input("What's your name? ").strip()
matches = re.search(r"^(.+), (.+)$", name)
if matches:
	name = matches.group(2) + " " + matches.group(1)
print(f"hello, {name}")
```
```python
import re

name = input("What's your name? ").strip()
matches = re.search(r"^(.+), *(.+)$", name)
if matches:
	name = matches.group(2) + " " + matches.group(1)
print(f"hello, {name}")
# " *" - a space, 0 or more repetitions
```
```python
import re

name = input("What's your name? ").strip()
if matches := re.search(r"^(.+), *(.+)$", name):
	name = matches.group(2) + " " + matches.group(1)
print(f"hello, {name}")
# `:=` operator assigns a value from right to left and allows us to ask a boolean question at the same time
```
# Extracting User Input:
```python
url = input("URL: ").strip()

username = url.replace("https://twitter.com/", "")
print(f"Username: {username}")
```
```python
url = input("URL: ").strip()

username = url.removeprefix("https://twitter.com/")
print(f"Username: {username}")
```
`re.sub(pattern, repl, string, count=0, flags=0)`
```python
import re

url = input("URL: ").strip()

username = re.sub(r"https://twitter.com/", "", url)
print(f"Username: {username}")
```
```python
import re

url = input("URL: ").strip()

username re.sub(r"^(https?://)?(www\.)?twitter\.com/", "", url)
print(f"Username: {username}")
# For the purpose of tolerating both `http` and `https`, we add a `?` to the end of `https?`, making the `s` optional
```
```python
import re

url = input("URL: ").strip()

matches = re.search(r"^https?://(www\.)?twitter\.com/(.+)$", url, re.IGNORECASE)
if matches:
	print(f"Username:", matches.group(2))
```
```python
import re

url = input("URL: ").strip()

if matches := re.search(r"^https?://(?:www\.)?twitter\.com/(.+)$", url, re.IGNORECASE):
	print(f"Username:", matches.group(1))
```
```python
import re

url = input("URL: ").strip()

if matches := re.search(r"^https?://(?:www\.)?twitter\.com/([a-z0-9_]+)", url, re.IGNORECASE):
	print(f"Username:", matches.group(1))
```
# OOP:
```python
def main():
	student = get_student()
	if student["name"] == "Padma":
		student["house"] = "Ravenclaw"
	print(f"{student['name']} from {student['house']}")


def get_student():
	name = input("Name: ")
	house = input("House: ")
	return {"name": name, "house": house}


if __name__ == "__main__":
	main()
```
## Classes:
```python
class Student:
	def __init__(self, name, house): #Student.self refers to the current object that has just been created
		self.name = name
		self.house = house


def main():
	student = get_student()
	print(f"{student.name} from {student.house}")


def get_student():
	student = Student()
	student.name = input("Name: ")
	student.house = input("House: ")
	return student


if __name__ == "__main__":
	main()
```

```python
class Student:
	def __init__(self, name, house):
		self.name = name
		self.house = house


def main():
	student = get_student()
	print(f"{student.name} from {student.house}")


def get_student():
	name = input("Name: ")
	house = input("House: ")
	return Student(name, house)


if __name__ == "__main__":
	main()
```
### raise:
```python
class Student:
	def __init__(self, name, house, patronus = None):
		if not name:
			raise ValueError("Missing name")
		if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
			if patronus and patronus not in ["Stag", "Otter", "Jack Russell terrier"]:
		raise ValueError("Invalid patronus")
		raise ValueError("Invalid house")
		
		self.name = name
		self.house = house
		self.patronus = patronus

	def __str__(self): #__str__ is built-in, comes with classes
		return f"{self.name} from {self.house}"

	def charm(self):
		match self.patronus:
			case "Stag":
				return ""
			case "Otter":
				return ""
			case "Jack Russell terrier":
				return ""
			case _:
				return ""


def main():
	student = get_student()
	print("Expecto Patronum!")
	print(student.charm())
	print(f"{student.name} from {student.house}")


def get_student():
	name = input("Name: ")
	house = input("House: ")
	patronus = input("Patronus: ") or None
	return Student(name, house, patronus)


if __name__ == "__main__":
	main()
```

### Decorators:
```python
class Student:
	def __init__(self, name, house):
		if not name:
			raise ValueError("Invalid name")
		self.name = name
		self.house = house

	def __str__(self):
		return f"{self.name} from {self.house}"

	# Getter for name
	@property
	def name(self):
		return self._name

	# Setter for name
	@name.setter
	def name(self, name):
		if not name:
			raise ValueError("Invalid name")
		self._name = name

	# Getter for house
	@property
	def house(self):
		return self._house #_house, "_", means that the value should not be modified directly (but using the house.setter)
	
	# Setter for house
	@house.setter
	def house(self, house):
		if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
			raise ValueError("Invalid house")
		self._house = house
		

def main():
	student = get_student()
	print(student)

def get_student():
	name = input("Name: ")
	house = input("House: ")
	return Student(name, house)

if __name__ == "__main__":
	main()
```
### Methods:
```python
import random


class Hat:
	def __init__(self):
		self.houses = ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]

	def sort(self, name):
		print(name, "is in", random.choice(self.houses))


hat = Hat()
hat.sort("Harry")
```

```python
import random


class Hat:

	houses = ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]

	@classmethod
	def sort(cls, name):
		print(name, "is in", random.choice(cls.houses))


Hat.sort("Harry")
```

```python
class Student:
	def __init__(self, name, house):
		self.name = name
		self.house = house

	def __str__(self):
		return f"{self.name} from {self.house}"

	@classmethod
	def get(cls):
		name = input("Name: ")
		house = input("House: ")
		return cls(name, house)


def main():
	student = Student.get()
	print(student)


if __name__ == "__main__":
	main()
```
### Inheritance:
```python
class Wizard:
	def __init__(self, name):
		if not name:
			raise ValueError("Missing name")
		self.name = name

	...


class Student(Wizard):
	def __init__(self, name, house):
		super().__init__(name) #runs the "init" method of "Wizard"
		self.house = house

	...


class Professor(Wizard):
	def __init__(self, name, subject):
		super().__init__(name)
		self.subject = subject

	...


wizard = Wizard("Albus")
student = Student("Harry", "Gryffindor")
professor = Professor("Severus", "Defense Against the Dark Arts")
...
```
### Operator Overloading:
- Some operators such as `+` and `-` can be “overloaded” such that they can have more abilities beyond simple arithmetic
```python
class Vault:
	def __init__(self, galleons=0, sickles=0, knuts=0):
		self.galleons = galleons
		self.sickles = sickles
		self.knuts = knuts

	def __str__(self):
		return f"{self.galleons} Galleons, {self.sickles} Sickles, {self.knuts} Knuts"

	def __add__(self, other):
		galleons = self.galleons + other.galleons
		sickles = self.sickles + other.sickles
		knuts = self.knuts + other.knuts
		return Vault(galleons, sickles, knuts)


potter = Vault(100, 50, 25)
print(potter)

weasley = Vault(25, 50, 100)
print(weasley)

total = potter + weasley
print(total)
```