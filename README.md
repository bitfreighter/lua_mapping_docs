# EDI Mapping Lua Functions

This documentation provides a list of custom Lua functions available for use in Lua-based EDI mapping scripts. These functions assist in transforming, manipulating, and handling EDI data efficiently.

---

## Table Functions

### `reduce(tab, initial, func)`
Reduces a table by applying a function cumulatively from left to right.

- **Parameters:**
  - `tab` (table): The input table.
  - `initial` (any): The starting value.
  - `func` (function): Takes `(value, accumulator)` as arguments.
- **Returns:** The final accumulated value.

**Example:**
```lua
local sum = reduce({1, 2, 3, 4}, 0, function(value, accum) return accum + value end)
-- sum = 10
```

---

### `map(tab, func)`
Applies a function to each element in a table.

- **Parameters:**
  - `tab` (table): The input table.
  - `func` (function): Applied to each element.
- **Returns:** A table with transformed elements.

**Example:**
```lua
local squared = map({1, 2, 3}, function(x) return x * x end)
-- squared = {1, 4, 9}
```

---

### `filter(tab, func)`
Filters elements of a table based on a condition.

- **Parameters:**
  - `tab` (table): The input table.
  - `func` (function): Returns `true` for elements to keep.
- **Returns:** A table with filtered elements.

**Example:**
```lua
local evens = filter({1, 2, 3, 4}, function(x) return x % 2 == 0 end)
-- evens = {2, 4}
```

---

### `find(tab, func)`
Finds the first element in a table that matches a condition.

- **Parameters:**
  - `tab` (table): The input table.
  - `func` (function): Returns `true` for a match.
- **Returns:** The first matching element or `nil`.

**Example:**
```lua
local first_even = find({1, 3, 5, 6}, function(x) return x % 2 == 0 end)
-- first_even = 6
```

---

### `table_contains(tbl, x)`
Checks if a table contains a value.

- **Parameters:**
  - `tbl` (table): The input table.
  - `x` (any): The value to check.
- **Returns:** `true` if found, otherwise `false`.

**Example:**
```lua
local exists = table_contains({10, 20, 30}, 20)
-- exists = true
```

---

### `table.compare(tbl1, tbl2)`
Compares two tables element-wise.

- **Parameters:**
  - `tbl1` (table): First table.
  - `tbl2` (table): Second table.
- **Returns:** `true` if tables match, `false` otherwise.

**Example:**
```lua
local same = table.compare({a = 1, b = 2}, {a = 1, b = 2})
-- same = true
```

---

## String Functions

### `string.trim(s)`
Removes leading and trailing spaces from a string.

- **Parameters:**
  - `s` (string): Input string.
- **Returns:** Trimmed string.

**Example:**
```lua
local trimmed = string.trim("  hello world  ")
-- trimmed = "hello world"
```

---

### `string.downcase(value)`
Converts a string to lowercase.

**Example:**
```lua
local lower = string.downcase("HELLO")
-- lower = "hello"
```

---

### `string.upcase(value)`
Converts a string to uppercase.

**Example:**
```lua
local upper = string.upcase("hello")
-- upper = "HELLO"
```

---

### `string.pad_leading(value, length, pad?)`
Pads a string at the beginning to the given length.

**Example:**
```lua
local padded = string.pad_leading("42", 5, "0")
-- padded = "00042"
```

---

### `string.pad_trailing(value, length, pad?)`
Pads a string at the end to the given length.

**Example:**
```lua
local padded = string.pad_trailing("42", 5, "0")
-- padded = "42000"
```

---

### `string.split(value, separator?)`
Splits a string into a table.

**Example:**
```lua
local parts = string.split("a,b,c", ",")
-- parts = {"a", "b", "c"}
```

---

## EDI-Specific Functions

### `edi.append(tx, version, position, segments)`
Appends segments at a specified position.

**Example:**
```lua
edi.append(tx, "4010", "H0100", new_segments)
```

---

### `edi.prepend(tx, version, position, segments)`
Works like `append` but prepends instead of appending.

---

### `edi.convert_timezone(segments, tz_code_list)`
Converts time zones in EDI segments.

---

### `edi.create_ms1s(segments, load)`
Creates an MS1 (location) segment.

---

### `edi.create_ms2s(segments, load)`
Creates an MS2 (shipment) segment.

---

### `edi.create_oids(map)`
Creates OID segments from order details.

---

### `edi.create_l3(segments, load)`
Creates an `L3` segment for load information.

---

### `edi.map_loops(segments, start_segment, version, type, func)`
Maps segments for a given loop defined by the EDI version.

---

### `edi.map_transactions(segments, function)`
Maps transactions from EDI segments.

---

### `edi.map_interchanges(segments, function)`
Maps interchanges from EDI segments.

---

### `edi.move(segments, version, old_pos, new_pos)`
Moves segment(s) from one position to another.

---

### `edi.remove_first_last_s5_loops(segments)`
Removes the first and last `S5` loops from the EDI segments.

---

### `edi.split_lx_transactions(segments)`
Splits `214` transactions that have multiple `LX` loops into separate transactions.

---

### `edi.city_state_to_lat_long(city, state)`
Gets latitude and longitude for a city/state.

**Example:**
```lua
local coords = edi.city_state_to_lat_long("New York", "NY")
-- coords = {latitude = 40.7128, longitude = -74.0060}
```

---

### `get_load_info(city, state)`
Gets load information from the database for the current transaction.

**Example:**
```lua
-- assuming segments is a transaction pertaining to a load (204/990/214/210)
local load_info = get_load_info(segments)
-- load_info is a table with information about the load including stops, reference numbers, etc.
```

---

## Debugging Functions

### `debug.log(term)`
Logs a Lua value to the console.

---

## Final Notes
- These functions work within Lua scripts used in EDI mapping.
- Table-based functions are useful for transformation.
- Date/time functions assist with EDI-compliant formatting.
- EDI functions manipulate segments and elements.
