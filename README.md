# Dataset of Operationalizing Advance-Postponement for Replenishment-Assembly Synchronization in VMI-ATO Systems under Demand-Forecast Evolution

A synthetic multi-period, multi-scenario benchmark dataset designed for the advance-postponement (AP) replenishment optimization problem in Vendor Managed Inventory–Assemble-to-Order (VMI-ATO) systems. This dataset is generated using rolling Martingale Model of Forecast Evolution (MMFE)-style demand forecasting and conditional scenario sampling. The public benchmark instances released in this repository use 15 products, 80 active materials/components, 8 decision periods, 8 scenarios for each decision period, and a rolling forecast horizon of 3 periods. This dataset is suitable for evaluating stochastic replenishment, inventory control, replenishment-assembly synchronization, and AP-based optimization algorithms such as the Memetic Adaptive Genetic Algorithm (MAGA).

## Dataset Structure

The dataset is organized as a series of Excel workbooks. Each workbook corresponds to one rolling decision period and provides the scenario forecasts, product-material structure, actual demand information, and rolling-state inputs required for AP-based replenishment optimization.

For a given decision period t, each scenario sheet represents one possible demand-forecast path generated under the MMFE-based rolling forecasting mechanism. Each scenario covers the current decision period and the next three forecast periods. Therefore, the rolling window contains four periods in total: the current period plus a 3-period look-ahead horizon.

The sheet descriptions below apply generally across the benchmark workbooks. Some sheets contain global parameters or global demand information, while others contain period-specific rolling states. Their meanings remain consistent across workbooks.

## Sheet Descriptions

### Scenario demand forecast sheets: `S{s}{t}`

`S{s}{t}` denotes the product-level demand forecast under scenario `s` at decision period `t`.

For example:

- `S11` denotes scenario 1 at decision period 1.
- `S82` denotes scenario 8 at decision period 2.
- `S38` denotes scenario 3 at decision period 8.

Each scenario sheet contains demand forecasts for the 15 products over the current period and the next three forecast periods. Rows represent products, while columns represent the rolling forecast periods. These sheets provide the stochastic product demand paths used in the AP replenishment optimization model.

### Product-material relationship sheet: `BOM`

`BOM` records the bill-of-materials relationship between products and materials/components. Rows represent products, and columns represent materials/components. In the released benchmark instances, the entries indicate whether a material/component is required by a product. This matrix is used to convert product-level demand into material/component-level demand.

### Actual product demand sheet: `AD`

`AD` records the realized product demand over the observed decision periods. Rows represent products, and columns represent actual work periods. This sheet provides the actual demand information used for rolling evaluation and state updating.

### Inventory cost sheet: `INV`

`INV` records the inventory holding cost parameter for each material/component. The values are used to calculate the cost of storing material/component inventory in the factory buffer area.

### Component volume sheet: `CV`

`CV` records the unit volume of each material/component. This parameter is used to calculate pallet capacity consumption, inventory storage requirements, and volume-related operational constraints.

### Overdue penalty cost sheet: `PC`

`PC` records the unit overdue penalty cost for each material/component. This parameter is used to evaluate the cost associated with delayed replenishment or unmet time-sensitive demand.

### Stockout cost sheet: `SHC`

`SHC` records the unit stockout cost for each material/component. This parameter is used to evaluate the cost caused by material/component shortages.

### Scenario probability sheet: `pro`

`pro` records the probability assigned to each scenario. In the released benchmark instances, eight scenarios are used for each decision period and are assigned equal probabilities.

### Actual material/component demand sheet: `mad`

`mad` records the realized material/component demand over the observed decision periods. It is derived from the actual product demand in `AD` and the product-material relationship in `BOM`. Rows represent materials/components, and columns represent work periods.

### Rolling stockout state sheet: `ASC{k}`

`ASC{k}` records the material/component stockout state carried from period `k` to the next rolling decision period. It represents the shortage quantity that remains unresolved before the current decision is made.

For example, `ASC1` records the stockout state after period 1 and serves as an input for the rolling decision at period 2.

### Rolling inventory state sheet: `AZ{k}`

`AZ{k}` records the material/component inventory state carried from period `k` to the next rolling decision period. It represents the on-hand inventory available before the current decision is made.

For example, `AZ1` records the inventory state after period 1 and serves as an input for the rolling decision at period 2.

### Rolling replenishment decision sheet: `X{k}`

`X{k}` records the replenishment decision or replenishment quantity associated with period `k`. It is used to maintain rolling-horizon continuity between consecutive decision periods and to support state updating in the AP replenishment optimization process.

For example, `X1` records the replenishment-related decision state after period 1 and serves as a rolling input for the subsequent decision period.

## Notes

- The released benchmark instances use 80 active materials/components.
- The scenario sheets provide product-level stochastic demand paths. Material/component-level demand can be obtained by multiplying product demand by the `BOM` matrix.
- The rolling-state sheets `ASC{k}`, `AZ{k}`, and `X{k}` support dynamic state transfer between consecutive decision periods.
- The dataset is intended for computational experiments on stochastic replenishment, inventory control, replenishment-assembly synchronization, and AP-based optimization in VMI-ATO systems.
