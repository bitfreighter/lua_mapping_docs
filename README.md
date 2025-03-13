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

## DateTime Functions

### `datetime.add_hours(date, time, hours)`
Adds hours to a date-time.

**Example:**
```lua
local new_date, new_time = datetime.add_hours("20240312", "1400", 5)
-- new_date = "20240312", new_time = "1900"
```

---

### `datetime.now()`
Returns the current date and time as a table.

**Example:**
```lua
local now = datetime.now()
-- now = {year = 2024, month = 3, day = 12, hour = 15, minute = 30}
```

---

## EDI-Specific Functions

### `edi.get_element(segments, element)`
Finds the first matching element in a segment.

**Example:**
```lua
local value = edi.get_element(segments, "B204")
```

---

### `edi.set_element(segments, element, value)`
Sets the value of an element in EDI segments.

**Example:**
```lua
edi.set_element(segments, "N104", "123456789")
```

---

### `edi.find_segments(segments, criteria)`
Finds segments matching criteria.

**Example:**
```lua
local matches = edi.find_segments(segments, "B2")
```

---

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

### `edi.city_state_to_lat_long(city, state)`
Gets latitude and longitude for a city/state.

**Example:**
```lua
local coords = edi.city_state_to_lat_long("New York", "NY")
-- coords = {latitude = 40.7128, longitude = -74.0060}
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

