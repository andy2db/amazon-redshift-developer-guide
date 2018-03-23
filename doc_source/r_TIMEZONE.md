# TIMEZONE Function<a name="r_TIMEZONE"></a>

TIMEZONE returns a time stamp for the specified time zone and time stamp value\.

## Syntax<a name="r_TIMEZONE-syntax"></a>

```
TIMEZONE ('timezone', { timestamp | timestamptz )
```

## Arguments<a name="r_TIMEZONE-arguments"></a>

*timezone*  
The time zone for the return value\. The time zone can be specified as a time zone name \(such as **'Africa/Kampala'** or **'Singapore'**\) or as a time zone abbreviation \(such as **'UTC'** or **'PDT'**\)\. To view a list of supported time zone names, execute the following command\.   

```
select pg_timezone_names();
```
 To view a list of supported time zone abbreviations, execute the following command\.   

```
select pg_timezone_abbrevs();
```
For more information and examples, see [Time Zone Usage Notes](CONVERT_TIMEZONE.md#CONVERT_TIMEZONE-usage-notes)\.

*timestamp*  
An expression that results in a TIMESTAMP type, or a value that can implicitly be coerced to a time stamp\.

*timestamptz*  
An expression that results in a TIMESTAMPTZ type, or a value that can implicitly be coerced to a time stamp with time zone\.

## Return Type<a name="r_TIMEZONE-return-type"></a>

TIMESTAMPTZ when used with a TIMESTAMP expression\. 

TIMESTAMP when used with a TIMESTAMPTZ expression\. 