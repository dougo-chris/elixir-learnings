## Web Parameters

### Undserscore Keys
```
def underscore_keys(nil), do: nil

def underscore_keys(map = %{}) do
  map
  |> Enum.map(fn {k, v} -> {Macro.underscore(k), underscore_keys(v)} end)
  |> Enum.into(%{})
end

# Walk the list and atomize the keys of
# of any map members
def underscore_keys([head | rest]) do
  [underscore_keys(head) | underscore_keys(rest)]
end

def underscore_keys(not_a_map) do
  not_a_map
end
```

### Covert params to atoms
Only convert allowed keys
```
def key_to_atom(map, allowed) do
  map
  |> Map.take(allowed)
  |> Enum.reduce(%{}, fn {key, value}, acc ->
    Map.put(acc, String.to_atom(key), value)
  end)
end
```
