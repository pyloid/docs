# Store

The `Store` class is a lightweight key-value database used by creating it via `app.store("store.json")` from a Pyloid app instance. You can store any Python object that is JSON serializable, and the data is persistently managed as a database file.

---

## Class Instantiation

```python
store = app.store("store.json")
```

- **app**: Pyloid instance (`Pyloid`)
- **"store.json"**: Path to the database file

---

## Methods

### 1. get

```python
store.get(key: str, default: Any = None) -> Any
```

#### Description
Returns the value associated with the specified key. If the key does not exist, returns `default`.

#### Parameters

- **key** (`str`): The key to retrieve
- **default** (`Any`): The default value to return if the key does not exist

#### Returns

- **Any**: The value stored for the key, or `default` if not found

#### Example

```python
from src.pyloid.pyloid import Pyloid

app = Pyloid(app_name="Pyloid-App")
store = app.store("store.json")

store.set("user", {"name": "Hong Gil-dong", "age": 30})
user = store.get("user")
print(user)  # {'name': 'Hong Gil-dong', 'age': 30}
print(store.get("nonexistent_key"))  # None
```

---

### 2. set

```python
store.set(key: str, value: Any) -> bool
```

#### Description
Adds or updates a key-value pair in the database. The value must be a JSON-serializable Python object.

#### Parameters

- **key** (`str`): The key to store
- **value** (`Any`): The value to store (must be JSON serializable)

#### Returns

- **bool**: Always returns `True`

#### Example

```python
store = app.store("store.json")
store.set("settings", {"theme": "dark", "notifications": True})
store.set("counter", 42)
store.set("items", ["apple", "banana", "orange"])
```

---

### 3. remove

```python
store.remove(key: str) -> bool
```

#### Description
Deletes the value associated with the specified key from the database.

#### Parameters

- **key** (`str`): The key to remove

#### Returns

- **bool**: Returns `True` if the key was deleted, `False` if the key did not exist

#### Example

```python
store = app.store("store.json")
store.set("temp", "temporary data")
store.remove("temp")  # True
store.remove("nonexistent_key")  # False
```

---

### 4. all

```python
store.all() -> List[str]
```

#### Description
Returns a list of all keys stored in the database.

#### Returns

- **List[str]**: A list of all stored keys

#### Example

```python
store = app.store("store.json")
store.set("key1", "value1")
store.set("key2", "value2")
keys = store.all()
print(keys)  # ['key1', 'key2']
```

---

### 5. purge

```python
store.purge() -> bool
```

#### Description
Deletes all keys and values from the database.

#### Returns

- **bool**: Always returns `True`

#### Example

```python
store = app.store("store.json")
store.set("key1", "value1")
store.set("key2", "value2")
store.purge()  # True
print(store.all())  # []
```

---

### 6. save

```python
store.save(option: Optional[int] = None) -> bool
```

#### Description
Saves the current state of the database to the file. You can specify orjson serialization options with the `option` parameter.

#### Parameters

- **option** (`Optional[int]`): (Optional) orjson.OPT_* flag

#### Returns

- **bool**: Returns `True` if saving was successful, `False` otherwise

#### Example

```python
store = app.store("store.json")
store.set("key", "value")
store.save()  # True
```

---

## Summary

- **Store** is created from a Pyloid app instance using `app.store("store.json")`.
- You can store any Python object that is JSON serializable, such as strings, numbers, lists, and dictionaries.
- Main methods: `get`, `set`, `remove`, `all`, `purge`, `save`
- Data is persistently managed as a database file.