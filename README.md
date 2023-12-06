# TypedDataTableConverter
A version of the JSON.NET DataTable converter that allows you to specify the data types of columns if known.

The default datatable converter will sometimes not accurately identify the type of column if the JSON being parsed has either a missing or ambiguously formatted value in the first row.

If you know the types of the values in the JSON file up front to the converter which will use these values rather than tying to infer them from the data. You can supply this information to the converted either as a dictionary of types keyed on the property names or as the type of the object the JSON represents. The converter will fall back to it's default mechanism for identifying a type if it cannot find a column type in the supplied values.

```
var typedConverter = new TypedDataTableConverter(typeof(Employee));
DataTable dataTable = JsonConvert.DeserializeObject<DataTable>(json, typedConverter);
```
or
``` 
var employeeDataTypes = new Dictionary<string, Type>();
employeeDataTypes["HireDate"] = typeof(DateTime);
employeeDataTypes["StartDate"] = typeof(DateTime);
employeeDataTypes["Active"] = typeof(bool);
employeeDataTypes["Salary"] = typeof(decimal);
var typedConverter = new TypedDataTableConverter(employeeDataTypes);
DataTable dataTable = JsonConvert.DeserializeObject<DataTable>(json, typedConverter);
```

The converter code is a direct copy of the Newtonsoft [repository code](https://github.com/JamesNK/Newtonsoft.Json/blob/master/Src/Newtonsoft.Json/Converters/DataTableConverter.cs) with a few small changes
