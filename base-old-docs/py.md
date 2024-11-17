<p align='center'><img src="https://contiguity.co/assets/icon-black.png" height="150px"/></p>
<h1 align='center'>@contiguity/base</h1>

<p align='center'>
    <img display="inline-block" src="https://img.shields.io/pypi/v/contiguity_base?style=for-the-badge" /> <img display="inline-block" src="https://img.shields.io/badge/Made%20with-Python-green?style=for-the-badge" />
</p>
<p align='center'>Contiguity's official Python SDK for Contiguity Base</p>

## Installation 🏗 & Setup 🛠
You can install the SDK using pip:
```shell
$ pip install contiguity_base
```

Then, import & initialize it like this:

```python
from contiguity_base import connect

db = connect("your-api-key", "your-project-id")
```

You can get an API key by fetching it in the [dashboard](https://base.contiguity.co), and a project ID is given to you when creating a project.

## <img src="https://avatars.githubusercontent.com/u/47275976?s=280&v=4" alt="Deta Logo" style="vertical-align: middle;" height="30"> For those moving from Deta Space <img src="https://avatars.githubusercontent.com/u/47275976?s=280&v=4" alt="Deta Logo" style="vertical-align: middle;" height="30">
Contiguity Base is a one-to-one replacement for the old Deta Base API, Deta Base JavaScript SDK, Deta Base Python SDK, and Deta Base Go SDK. The only thing that has changed is initialization. 

Instead of `deta = Deta(project_key)`, you'll use `db = connect(api_key, project_id)`

The rest stays the same, because at Contiguity, we think it's crazy for a cloud provider to give you 45 days to move dozens of apps from their proprietary database.

If you're transitioning from Deta Space to Contiguity, welcome! 

## Creating your first "base" 📊

To start working with a base, you can create a Base instance:

```python
my_base = db.Base("my-awesome-base")
```

Now you're ready to perform some cool database operations!

## Putting data into your base 📥

To add an item to your base, use the `put` method:

```python
item = {
    "name": "Contiguity",
    "is_awesome": True,
    "coolness_level": 9000
}

my_base.put(item)
```

You can also specify a key for your item:

```python
my_base.put(item, "unique-key-1")
```

## Batch putting 📦
Need to add multiple items at once? No problem! Just pass a list of items:

```python
items = [
    {"name": "Item 1", "value": 100},
    {"name": "Item 2", "value": 200},
    {"name": "Item 3", "value": 300, "key": "some-unique-key"}
]

my_base.put(items)
```

## Inserting data into your base 🚀
To insert an item into your base, use the insert method. This is useful when you want to ensure you're not overwriting existing data:
```python
new_item = {
    "name": "New Product",
    "price": 49.99
}

my_base.insert(new_item, "product-1")
```

If an item with the same key already exists, the insert operation will fail, preventing accidental overwrites.

## Getting data from your base 🔍

To retrieve an item, use the `get` method:

```python
my_item = my_base.get("unique-key-1")
print(my_item["name"])  # Outputs: Contiguity
```

## Updating data in your base 🔄

Need to update an item? Use the `update` method:

```python
my_base.update({"coolness_level": 9001}, "unique-key-1")
```

## Deleting data from your base 🗑️

To remove an item, use the `delete` method:

```python
my_base.delete("unique-key-1")
```

## Querying (fetching) your base 🕵️‍♀️

You can perform complex queries using the `fetch` method like so:

```python
results = my_base.fetch({
    "is_awesome": True,
    "profile.name?contains": "John"
})
```

### Query Operators

#### Equal

```python
{
  "age": 22, 
  "name": "Sarah"
}
```

- **Hierarchical**  
```python
{
  "user.profile.age": 22, 
  "user.profile.name": "Sarah"
}
```

- **Array**  
```python
{
  "fav_numbers": [2, 4, 8]
}
```

- **Nested Object**  
```python
{
  "time": { 
    "day": "Tuesday", 
    "hour": "08:00"
  }
}
```

#### Not Equal

```python
{
  "user.profile.age?ne": 22
}
```

#### Less Than

```python
{
  "user.profile.age?lt": 22
}
```

#### Greater Than

```python
{
  "user.profile.age?gt": 22
}
```

#### Less Than or Equal

```python
{
  "user.profile.age?lte": 22
}
```

#### Greater Than or Equal

```python
{
  "user.profile.age?gte": 22
}
```

#### Prefix (String starts with)

```python
{
  "user.id?pfx": "afdk"
}
```

#### Range

```python
{
  "user.age?r": [22, 30]
}
```

#### Contains

- **String contains a substring**  
```python
{
  "user.email?contains": "@contiguity.co"
}
```

- **List contains an item**  
```python
{
  "user.places_lived_list?contains": "Miami"
}
```

#### Not Contains

- **String does not contain a substring**  
```python
{
  "user.email?not_contains": "@contiguity.co"
}
```

- **List does not contain an item**  
```python
{
  "user.places_lived_list?not_contains": "Miami"
}
```

## Utility operations 🛠️

Contiguity provides some cool utility operations for updating your data:

### Increment a value
```python
my_base.update({"views": my_base.util.increment(1)}, "blog-post-1")
```

### Decrement a value
```python
my_base.update({"days": my_base.util.increment(-1)}, "countdown")
```

### Append to an array
```python
my_base.update({"tags": my_base.util.append("awesome")}, "product-1")
```

### Prepend to an array
```python
my_base.update({"recent_visitors": my_base.util.prepend("Alice")}, "website-stats")
```

### Trim a string
```python
my_base.update({"description": my_base.util.trim()}, "user-bio")
```

## Debug mode 🐛

If you enable debug mode during initialization, the SDK will log detailed information about your requests. This can be super helpful for troubleshooting!
```python
db = connect("your-api-key", "your-project-id", debug=True)
```

## Error handling 🚨

The SDK won't throw errors when things don't go as planned. Instead, it will return None in most cases, like if you attempt to GET a non-existent key. However, it is always recommended to put database calls in a try/except block:

```python
try:
    my_base.get("non-existent-key")
except Exception as error:
    print("Oops!", str(error))
```

## Roadmap 🚦
- Support for more complex query operations
- Batch operations for deleting multiple items
- "Deta Drive" support (file storage)
- And many more exciting features!
