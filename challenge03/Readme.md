
### Challenge 03

We have a nested object, we would like a function that you pass in the object and a key and get
back the value. How this is implemented is up to you.
Example Inputs
object = {“a”:{“b”:{“c”:”d”}}}
key = a/b/c
object = {“x”:{“y”:{“z”:”a”}}}
key = x/y/z
value = a

##### Solution

json_search_func -> file contains the function to retreive given key from json object

**testing**

```
cd challenge03/

source json_search_func

root@MSI# object='{"x":{"y":{"z":"a"}},"p":"b","c":"ui"}'
root@MSI# key='"y"'
root@MSI#
root@MSI# searchkeyval $object $key
"y" -> {"z":"a"}


root@MSI# object='{"x":{"y":{"z":"a"}},"p":"b","c":"ui"}'
root@MSI# key='"c"'
root@MSI#
root@MSI# searchkeyval $object $key
"c" -> "ui"

```