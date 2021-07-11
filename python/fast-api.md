# Routes and views
- routes are defined within view method parameters
- views can be `async` methods
- request params are defined within route `@app` decorators and in method params
- query params are defined only in method params (`?a=b&c=False`)
- return json, list, string, int

## Basic app
```py
from fastapi import FastAPI

app = FastAPI()

@app.get('/')
async def root():
    return {"message":"you are at home"}

@app.get('/salon/{id}')
def getSalon(id:int, active:bool=True):
    return ['Salon of id if it is True by default']
```

## *Need to specify order of urls as it may lead to problems* 
---
example
```py
@app.get('/url/me')
# ----
@app.get('/url/{id}')
```


# Request Body
- the request body can be specified by using a pydantic model class as paramerter in the controller method.
```py
from pydantic import BaseModel
from fastapi import FastAPI
from typing import Optional
app = FastAPI()

class Item(BaseModel):
    id: int
    name: str
    tax: Optional[str] = None

@app.get('/root/{id}')
def root(id:int=None, item:Optional[Item]=None):
    return {"item":**item.dict()}
```