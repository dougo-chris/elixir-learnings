## Date & Time Attributes

### simple counter
```
defmodule MyCounter do
  def setup do
    :ets.new(:test, [:named_table])
  end

  def inc do
    case :ets.lookup(:test, :my_func) do
      [{_, value}] ->
        :ets.insert(:test, {:my_func, value + 1})
      _ ->
      :ets.insert(:test, {:my_func, 1})
    end
  end

  def count
    case :ets.lookup(:test, :my_func) do
      [{_, value}] ->
        value
      _ ->
        0
    end
  end
end
```