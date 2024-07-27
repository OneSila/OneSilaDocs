# Translatable Models

For translation we have a Translatable model structure.  There is a bit of setup for this - so let's have a look at the following minimal example:

## Models

First of all, create your models and add the right mixins:

- TranslatedModelMixin for the base model
- TranslationFieldsMixin for the translations

Let's make an example with a model `Table` where we add:

1. Mixins
2. Meta class settings
3. property to get the name by default from the translation model

```python
from translations.models import TranslationFieldsMixin, TranslatedModelMixin
from core import models

class Table(TranslatedModelMixin, models.Model):
    @property
    def name(self):
        return self._get_translated_value(field_name='name')


class TableTranslation(TranslationFieldsMixin, models.Model):
    table = models.ForeignKey(Table, on_delete=models.CASCADE)
    name = models.CharField(max_length=100)

    class Meta:
        unique_together = ['lead_time', 'language']
```



## Schema

Once you have set up the models, it's time to adjust your schema layer.
Assuming you have created the schema layer as per usual, we will make some adjustments:


First, open `yourapp/schema/types/type.py` and to your type, expose the property "name" you added on the model.

```python
@type(Table, filters=TableFilter, order=TableLeadTimeOrder, pagination=True, fields="__all__")
class TableType(relay.Node, GetQuerysetMultiTenantMixin):
    ...
    @field
    def name(self) -> str | None:
        return self.name

```

Next, when creating via graphql, you also want to make sure a default name is given.
edit `yourapp/schema/types/input.py` and add the name field as required.

```python
@input(Table, fields="__all__")
class TableInput:
    ...
    name: str
```


Finally, adjust `yourapp/schema/mutations.py` and make it translation compatible.

```python
...
from translations.schema.mutations import TranslatableCreateMutation
from yourapp.models import TableTranslation
from yourapp.schema.types.input import TableInput
from yourapp.schema.types.types import TableType

def create_table():
    extensions = []
    return TranslatableCreateMutation(TableInput,
        extensions=extensions,
        translation_model=TableTranslation,
        translation_field='name',
        translation_model_to_model_field='lead_time')

@type(name="Mutation")
class YourAppMutation:
    ...
    create_table: TableType = create_table()

```
