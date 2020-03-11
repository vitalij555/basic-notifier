![Upload Python Package](https://github.com/vitalij555/event-notifier/workflows/Upload%20Python%20Package/badge.svg)

# event-notifier

Simple python notifier.

## Contents

- [Background](#background)
- [Installation](#installation)
- [Usage](#usage)
- [Constructor](#constructor)
- [API Overview](#api-overview)
- [Tests](#tests)
- [License](#license)
- [Contributing](#contributing)

## Background

This is event notifier (sometimes called emitter) allowing to notify one or many subscribers about something that just happen.
Allows to use variable number of arguments. Is thread-safe. 

## Installation

```
pip install -U event-notifier
```

## Usage

```python
from EventNotifier import Notifier


class FileWatchDog():
	def onOpen(self, fileName, openMode):
		print(f"File {fileName} opened with {openMode} mode")
		
			
	def onClose(self, fileName):
		print(f"File {fileName} closed")
	

watchDog = FileWatchDog()	
	
	
notifier = Notifier(["onCreate", "onOpen", "onModify", "onClose", "onDelete"])

notifier.subscribe("onOpen",  watchDog.onOpen)
notifier.subscribe("onClose", watchDog.onClose)

notifier.fireEvent("onOpen", openMode="w+", fileName="test_file.txt")  # order of named parameters is not important
notifier.fireEvent("onClose", fileName="test_file.txt")
```
Will produce:
```console
$ python test.py
File test_file.txt opened with w+ mode
File test_file.txt closed
```

## Constructor

```python
Notifier(eventNames, logger=None)
```

**Parameters**

- `eventNames` - `list of any` - mandatory, provides list of all supported events. Values provided here can be used for raising events later.
 Values provided in this list can be of any type.
- `logger` - `object` - optional, logger supporting standard logging methods (info, warning error, etc..), default: `None`. 
If None is provided, then internal logger outputting warnings and errors to console will be created.


## API Overview

### subscribe(eventName, subscriber)

**Description**

Adds callable subscribers interested in some particular event. 

**Parameters**

- `eventName` - `any` - mandatory, specifies event, subscriber will be interested in.
- `subscriber` - `any` - mandatory, callable subscriber (function, class method or class with __call__ implemented)

**Example**




### fireEvent(eventName, *args, **kwargs)

**Description**



**Parameters**

- `eventName` - `any` - mandatory, provides list of all supported events. Values provided here later can be used for raising events  
- `*args` - `list` - optional, logger supporting standard logging methods (info, warning error, etc..), default: `None`
- `**kwargs` - `dictionary` - optional, logger supporting standard logging methods (info, warning error, etc..), default: `None`

**Example**


### removeSubscribersByEventName(eventName)

**Description**

**Parameters**

- `url` - `string` - optional, Events API URL, default: `None`


**Example**


### removeAllSubscribers()

**Description**

**Parameters**

- `url` - `string` - optional, Events API URL, default: `None`


**Example**







## Tests

[PyTest][pytest] is used for tests. Python 2 is not supported.

**Install PyTest**

```sh
$ pip install pytest
```

**Run tests**

```sh
$ py.test test/*
```

[pytest]: http://pytest.org/


## License

License
Copyright (C) 2020 Vitalij Gotovskij

event-notifier binaries and source code can be used according to the MIT License


## Contribute
TBD
