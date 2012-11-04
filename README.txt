This is an extension of the project JavaCSV hosted here:
http://sourceforge.net/projects/javacsv

The last version is 2.1 and has not been updated since 2011-01-23.

The issue with this version is that it does not allow the user to set a String
delimiter as the record separator of the CsvWriter. This represents no issue at
all for Windows users as the default delimiter is used in those cases.

For some reason, the default delimiter is indeed a String while the one the
user can set is only a char. This means that if a Windows user uses the default
line separator, the output will use the \r\n String. Additionally, Windows
users can use all the other separators (\n for Unix, \r for old Apple hardware)
as they are all only one char.

However, when not using Windows, the default separator becomes a String that
contains \r or \n. As the method setRecordDelimiter only allows to set a char,
a Unix user (as it is in my case), can not output CSV files with Windows line
separators.

This motivated me to change the CsvWriter class so that it supports setting
String line separators instead of only char.

NOTE: I did not change the CsvReader class. That means it works exactly the
same way as it used to. So, if you want to force a \r\n as a line separator
then you won't be able to do that as the method setRecordDelimiter for the
CsvReader class is unchanged. Please, feel free to improve this.