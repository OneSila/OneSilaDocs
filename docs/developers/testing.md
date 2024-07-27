# Testing your code

To test the code, there are some classes you can import to ensure you are using the right environments.

## Testing models

We have two available TestCase classes.

1. Without demo-data / blank

	```
	from core.tests import TestCaseWithDemoData
	```

2. With demo-data

	```
	from core.tests import TestCase
	```


## Testing Graphql schemas

```
from core.tests.tests_schemas.tests_queries import TransactionTestCaseMixin
```

of course you can combine it with the demo-data mixin:

```
from core.tests import TestCaseWithDemoData
```

Example:

```
from core.tests.tests_schemas.tests_queries import TransactionTestCaseMixin
from core.tests import TestCaseWithDemoData

class MyAppSchemaQueryTestCase(TestCaseWithDemoData, TransactionTestCaseMixin):
    def test_my_function(self):
        pass
```