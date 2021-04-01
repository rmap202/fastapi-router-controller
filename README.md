# What this repository contains
#### A FastAPI utility to allow Controller Class usage

## Installation: 

install the package
```
pip install fastapi-router-controller
```

## How to use

In a Class module

```python
from fastapi import APIRouter, Depends
from fastapi_router_controller import Controller

router = APIRouter()
controller = Controller(router)

async def amazing_fn():
    return 'amazing_variable'

@controller.resource()
class ExampleController():
    # you can define in the Controller init some FastApi Dependency and them are automatically loaded in controller methods
    def __init__(self, x: Foo = Depends(amazing_fn)):
        self.x = x
    
    @controller.route.get(
        '/some_aoi', 
        summary='A sample description')
    def sample_api(self):
        print(self.x) # -> amazing_variable
        
        return 'A sample response'
```

Load the controller to the main FastAPI app
```python
from fastapi import FastAPI
from fastapi_router_controller import Controller

import ExampleController

app = FastAPI(
    title='A sample application using fastapi_router_controller',
    version="0.1.0")

example_controller = ExampleController()
app.include_router(example_controller.router())
```

## For some Example use-cases visit the example folder