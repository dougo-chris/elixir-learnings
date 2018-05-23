## Enum

### Keyword Lists
```
list = [topic_id: "can't be blank", created_by: "can't be blank"]

# convert to a map
Enum.into(list, %{})

```


### Maps
```
map = %{one: 1, two: two}

# convert values
Map.new(map, fn {key, value} ->
  {key, to_string(value)}
end)

# select only required
Map.take(map, [:one, :three])

```