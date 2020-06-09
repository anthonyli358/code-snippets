# Python DevOps

## Azure

### Inference schema

```python
from inference_schema.schema_decorators import input_schema, output_schema
from inference_schema.parameter_types.standard_py_parameter_type import StandardPythonParameterType

def init():
	return

# include swagger, actual json input is of the form {request: {input_sample}}
input_sample = {}
output_sample = {}
@input_schema('request, StandardPythonParameterType(input_sample)  
@output_schema('request, StandardPythonParameterType(output_sample)
def run(request):
	return {}  # upon failure returns internal error 500 by default
```
