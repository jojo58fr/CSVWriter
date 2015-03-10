# CSVWriter
Simple c++ csv writer class.
## How to use ?
#### write a single row
```c++
CSVWriter csv;
csv << "this" << "is" << "a" << "row";
cout << csv << endl;
```
output:
```
this;is;a;row
```

#### write multiple rows
```c++
CSVWriter csv;
csv.newRow() << "this" << "is" << "the" << "first" << "row";
csv.newRow() << "this" << "is" << "the" << "second" << "row";
cout << csv << endl;
```
output
```
this;is;the;first;row
this;is;the;second;row
```
#### auto row
When each row has a fixed number of colums, CSVWriter can add rows automatic. In this example, every row has 4 colums
```c++
CSVWriter csv;
csv.enableAutoNewRow(5);
csv << "this" << "is" << "the" << "first" << "row" << "this" << "is" << "the" << "second" << "row";
cout << csv << endl;
```
output
```
this;is;the;first;row
this;is;the;second;row
```
#### write csv to filesystem
```c++
CSVWriter csv;
csv.newRow() << "this" << "is" << "the" << "first" << "row";
csv.newRow() << "this" << "is" << "the" << "second" << "row";
csv.writeToFile("foobar.csv");
```
#### append csv to existing file
```c++
CSVWriter csv;
csv << "append" << "this" << "row" << "please" << ":)";
cout << csv.writeToFile("foobar.csv",true) << endl;
```
#### change seperator
```
CSVWriter csv(",");
csv << "this" << "is" << "a" << "row";
cout << csv << endl;
```
output:
```
this,is,a,row
```
#### merge two CSVWriters
```c++
CSVWriter csv_a;
CSVWriter csv_b;
csv_a << "this" << "comes" << "from" << "csv_a";
csv_b << "this" << "is" << "from" << "csv_b";
csv_b += csv_a;
cout << csv_b << endl;
```
output
```
this;is;from;csv_b
this;comes;from;csv_a
```
#### supported datatypes
CSVWriter uses a `stringstream` so serilize values. Each datatype supported by `<<` operator from `stringstresm` can be used.
```c++
char c = 'c';
bool b = false;
short s = 6000;
int i = 300000;
float f = 3.14159;
double d = 4.85875e-270;
string str = "hello world";
char c_str[] = "whats up";
CSVWriter csv;
csv << c << b << s << i << f << d << str << c_str ;
cout << csv;
```
output
```
c;0;6000;300000;3.14159;4.85875e-270;hello world;whats up
```
As you can see, boolean values are serilized to `0` for `false` and `1` for `true`.
