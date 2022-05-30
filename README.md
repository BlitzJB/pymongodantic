# pymongodantic

<div align="center">

[![Build status](https://github.com/blitzjb/pymongodantic/workflows/build/badge.svg?branch=master&event=push)](https://github.com/blitzjb/pymongodantic/actions?query=workflow%3Abuild)
[![Python Version](https://img.shields.io/pypi/pyversions/pymongodantic.svg)](https://pypi.org/project/pymongodantic/)
[![Dependencies Status](https://img.shields.io/badge/dependencies-up%20to%20date-brightgreen.svg)](https://github.com/blitzjb/pymongodantic/pulls?utf8=%E2%9C%93&q=is%3Apr%20author%3Aapp%2Fdependabot)

[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Security: bandit](https://img.shields.io/badge/security-bandit-green.svg)](https://github.com/PyCQA/bandit)
[![Pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/blitzjb/pymongodantic/blob/master/.pre-commit-config.yaml)
[![Semantic Versions](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--versions-e10079.svg)](https://github.com/blitzjb/pymongodantic/releases)
[![License](https://img.shields.io/github/license/blitzjb/pymongodantic)](https://github.com/blitzjb/pymongodantic/blob/master/LICENSE)
![Coverage Report](assets/images/coverage.svg)

`pymongodantic` is a MongoDB ORM working with pydantic thus being directly compatible with tools like FastAPI

</div>

### Example

```py
from pymongodantic.collection import Collection
from pymongo import MongoClient

client = MongoClient('mongodb+srv://LINK')
db = client.get_database('pymongodantictesting')
nicecollection = db.get_collection('nicecollection')


class TestModel(Collection):
    _collection = nicecollection
    id: int
    test_name: str


if __name__ == '__main__':
    test1 = TestModel(id=1, test_name='wowdude')
    test2 = TestModel(id=2, test_name='wowdudeeee')
    test1.insert_self()
    TestModel.insert_one(test2)
    TestModel.insert_many([test1, test2])
    print(TestModel.find_one({'test_name': 'wowdude'}))
    # Supports all the same methods as pymongo.collection.Collection
```