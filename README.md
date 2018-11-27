# Janrain Python API

A python implementation of the Janrain configuration API to allow simpe creating and management of clients, flows and schemas

## Setup

The API uses a series of environment variables to execute queries and changes. These are the required environment variables

| Variable                   | Contents                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------|
| JANRAIN_REGION             | The region where the Janrain instance is running. This is available on the console homepage                         |
| JANRAIN_APP                | The ID of the Janrain application instance. This is available on the console homepage                               |
| JANRAIN_CLIENT             | The client ID to use to execute the queries and updates. This is available under "Manage Properties" in the console |
| JANRAIN_SECRET             | The secret assigned to the above client ID, this is available under "Manage Properties" in the console              |
| JANRAIN_REGISTRATION_REALM | The registration realm which is given to an Janrain instance. It's sometimes referred to application name           |

## Getting Started

#### Installation

Installing this package is done directly from github for now, so the full URL is required in the `pip install` command

```
pip install git+https://github.com/amido/janrain-python-api.git#egg=janrain-python-api
```

Using the above environment variables in API calls is easy. Import the API and set these in the `defaults{}` which are then passed to the api, like so:

```python
import os
from janrain.api import Api


defaults = {
    'janrain_region':             os.environ['JANRAIN_REGION'],
    'janrain_app':                os.environ['JANRAIN_APP'],
    'janrain_id':                 os.environ['JANRAIN_CLIENT'],
    'janrain_secret':             os.environ['JANRAIN_SECRET'],
    'janrain_registration_realm': os.environ['JANRAIN_REGISTRATION_REALM']
}

api = Api(defaults)
```

# Documentation

Documentation has been automatically generated by [pydoc-markdown](https://github.com/NiklasRosenstein/pydoc-markdown) to give examples of inputs and outputs. It is found at [DOCUMENTATION.md](DOCUMENTATION.md)

### Updating Documentation

After making changes to the API, rebuild the documnetation with the following command from the root of the project:

`pydocmd simple janrain.api++ > DOCUMENTATION.md`

# Examples

**Arguments and data supplied to and from the API can be found in the official [Janrain Documentation](https://docs.janrain.com/api/registration/config/#)**

### Getting All Clients

```python
api.get_clients()
```

_This will return a json object of all the clients with data from Janrain_

### Creating A Client

```python
client_file = open("janrain-client.json", "r")
client_json = json.load(client_file)
api.create_client(client_json)
```

_Creating a client requires a simple JSON object, which we recommend storing as a file to be read_