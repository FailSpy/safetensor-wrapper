# Safetensor Wrapper

A lightweight command-line tool and Python wrapper for managing Safetensors files, commonly used to store tensor data in machine learning models. This utility allows you to read metadata, list tensors, and generate tensor indices across one or more Safetensors files.

## CLI tool Features
- **Read Metadata**: Extracts and displays the JSON metadata from a Safetensors file.
- **List Tensors**: Lists all tensor names in one or more Safetensors files.
- **Generate Index**: Creates a JSON index containing the total size and tensor-file mapping.

## Usage

### Command-line Interface (CLI)
You can use the following commands to interact with Safetensors files:

- **Read Metadata**:
  ```bash
  python safetensor_utils.py metadata <path_to_file.safetensors>
  ```
  Reads out tensor info as stored by the Safetensor format such as dtype, shape, and offsets
  
- **List Tensors**:
  ```bash
  python safetensor_utils.py list <file1.safetensors> <file2.safetensors>
  ```
  Lists tensors purely by name
  
- **Generate Index**:
  ```bash
  python safetensor_utils.py index <file1.safetensors> <file2.safetensors>
  ```
  This returns a JSON index of metadata and weight_map, similar to `model.safetensors.index.json` you'll sometimes see on model repos.

### As a Python Library
You can also use this tool programmatically:

```python
from safetensors_utilities import SafeTensorsWrapper, read_safetensors_json

# Read metadata from safetensor header
metadata = read_safetensors_json('path_to_file.safetensors')

# List tensors
wrapper = SafeTensorsWrapper(['file1.safetensors'])
tensor_names = wrapper.keys()

# Access a tensor by name
tensor = wrapper['tensor_name']

# Lazy loop through tensors
for tensor in wrapper:
  print(tensor)

# Fully load all tensors as a dict:
state_dict = dict(wrapper)

# Generate safetensors.index.json structure as Python dict
index = wrapper.get_index()
```

## License
This project is licensed under the MIT License.
