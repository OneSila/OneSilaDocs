# Adding demo data

We have a core registry to add demo-data to the apps that need/use it. 
In order to use the registry, there are a few simple things to keep in mind:

## Base setup.

First of all, create a file called demo_data.py in your app.
In that file, you will need to call the registry:

    ```python
    from core.demo_data import DemoDataLibrary
    
    registry = DemoDataLibrary()
    ```

Once you haved called the registry, there are two ways to create demo-data.

- class based
- function based

## Class based demo data

The simplest way to generate data for a simple model is to declare some settings and map the field.  Once done, register you class.

    ```python
    from core.demo_data import fake, PrivateDataGenerator

    class AppMyModelGenerator(PrivateDataGenerator):
        model = MyModel
        count = 1
        field_mapper = {
            'name': fake.name,
            'unit': fake.unit,
       }
    registry.register_private_app(AppMyModelGenerator)
    ```

This class based approach will no only create the demo-data but also make sure it is tracked and removable.
If however you have a more comnplex case, you can either choose to override the individual functions in the class - or simply use the class-based approach.

## Function based demo data.

For more complex use-cases you can create your own functions that will generate the data.  There are a few things to keep in mind:

    - Ensure you are tracking every create with `registry.create_demo_data_relation(instance)` to ensure it can also be removed.
    - multi_tenant_company is a required argument, and you only create on these companies.
    - you register your function via `registry.register_private_app(function)`


## Generating demo-data manually

### Creating

Want to manually trigger demo-data?

    ```python
    from core.models import MultiTenantCompany
    from core.demo_data import DemoDataLibrary

    mtc = MultiTenantCompany.objects.last()

    registry = DemoDataLibrary()
    registry.run(multi_tenant_company=mtc)
    ```

### Deleting

And to delete it:

    ```python
    from core.models import MultiTenantCompany
    from core.demo_data import DemoDataLibrary

    mtc = MultiTenantCompany.objects.last()

    registry = DemoDataLibrary()
    registry.delete_demo_data(multi_tenant_company=mtc)
    ```