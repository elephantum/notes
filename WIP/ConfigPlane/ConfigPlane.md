```python
# TODO take a look how nosql API looks like (mongo/redis)
# creates repo and pulls from git if necessary
configs = ConfigRepo.create()

# returns dict
await configs.get("config_a")
# returns pydantic model
await configs.get("config_b", PydanticConfigModel)
# returns CustomAdapter.from_bytes
await configs.get("config_d", CustomAdapter)

# automatically converts to json
await configs.set("config_c", dict_or_model)
# uses CustomAdapter.to_bytes
await configs.set("config_d", obj, CustomAdapter)

# сохраняет изменения и пушит их в гит
await configs.commit()

# pulls changes from git if applicable
await configs.pull()
```
