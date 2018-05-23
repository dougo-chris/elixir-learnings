## Date & Time Attributes

### Unix Timestamp
```
timestamp = DateTime.to_unix(DateTime.utc_now)
DateTime.from_unix(timestamp)
```

### DateTime
```
datetime = DateTime.utc_now
datetime.year
datetime.month
datetime.day
datetime.hour
datetime.minute
datetime.second
```

### Comparing dates
Comparisons in Elixir using ==, >, < and similar are structural and based on the Date struct fields.
For proper comparison between dates, use the **compare/2** function.

### Sleep

```
:timer.sleep(10)
```

### Convert to string (and timzezone)

```
  alias Timex.Timezone

  def date_raw(timestamp, tz) do
    date_raw =
      timestamp
      |> Timex.to_datetime()
      |> shift_tz!(tz)
      |> Timex.format("%Y:%m:%d", :strftime)

    case date_raw do
      {:ok, value} -> value
      _ -> nil
    end
  end

  def time_raw(timestamp, tz) do
    time_raw =
      timestamp
      |> Timex.to_datetime()
      |> shift_tz!(tz)
      |> Timex.format("%k:%m:%S", :strftime)

    case time_raw do
      {:ok, value} -> value
      _ -> nil
    end
  end

  def shift_tz!(_, nil), do: nil

  def shift_tz!(_, ""), do: nil

  def shift_tz!(timestamp, tz) do
    case Timezone.convert(timestamp, tz) do
      {:error, _} -> timestamp
      timestamp -> timestamp
    end
  end
```

### Convert to DateTime

```
def convert_to_datetime(value) when is_binary(value) do
  case Timex.parse(value, "%Y:%m:%d", :strftime) do
    {:ok, value} ->
      value
      |> Timex.to_datetime()
      |> convert_to_datetime()
    _ ->
      {:error, "Invalid value"}
  end
end

def convert_to_datetime(%Date{} = value) do
  convert_to_datetime(Timex.to_datetime(value))
end

def convert_to_datetime(%NaiveDateTime{} = value) do
  convert_to_datetime(Timex.to_datetime(value))
end

def convert_to_datetime(%DateTime{} = value) do
  {:ok, value}
end

def convert_to_datetime(_value), do: {:error, "Invalid value"}

```