# Solar and Storage

# TODO this is private for the moment as I (Peter Dudfield) have worked on this before
and need to check with old employer. There is enough public code that I don't think this is a problem

A Python Library to run solar and storage optimization.
This uses mixed integer linear programming and maximises revenue made by charging and discharging the battery.
The model uses variable prices and a solar generation profile.

Thanks you to the follow repos for inspiration
- https://github.com/ADGEfficiency/energy-py-linear
- https://github.com/wzyfrank/battery/
- https://github.com/greysonchung/Battery-Optimisation/
- https://github.com/edu230991/battery-optimization/

## Installation

# TODO


## Example

Import the packages and make some fake solar and price data
```
import numpy as np
import plotly.graph_objects as go
from plotly.subplots import make_subplots

from solar_and_storage.solar_and_storage import SolarAndStorage

```
Make the fake price and solar data
```

hours_per_day = 24


# make prices
prices = np.zeros(hours_per_day) + 30
prices[6:19] = 40
prices[9] = 50
prices[12:14] = 30
prices[16:18] = 50
prices[17] = 60

# make solar profile
solar = np.zeros(hours_per_day)
solar[8:16] = 2.0
solar[10:14] = 4.0
```

Then run optimization
```
solar_and_storage = SolarAndStorage(prices=prices, solar_generation=list(solar))
solar_and_storage.run_optimization()
result_df = solar_and_storage.get_results()
```



Now plot the data
```
fig = make_subplots(rows=3, cols=1, subplot_titles=["Solar profile", "Price", "SOC"])
fig.add_trace(go.Scatter(y=e_soc[:24], name="SOC"), row=3, col=1)
fig.add_trace(go.Scatter(y=solar, name="solar", line_shape="hv"), row=1, col=1)
fig.add_trace(
    go.Scatter(y=solar_power_to_grid, name="solar to gird", line_shape="hv"), row=1, col=1
)
fig.add_trace(go.Scatter(y=prices, name="price", line_shape="hv"), row=2, col=1)


fig.show(rendered="browser")
```

![Example](examples/solar_and_storage.png)

You can see that the battery charged from the solar site at the end of the solar maximum



