## Date & Time

** Adjust and convert a timestamp **

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


  defp shift_tz!(_, nil), do: nil
  defp shift_tz!(_, ""), do: nil

  defp shift_tz!(timestamp, tz) do
    case Timezone.convert(timestamp, tz) do
      {:error, _} -> timestamp
      timestamp -> timestamp
    end
  end
```