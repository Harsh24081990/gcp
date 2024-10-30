##### In BigQuery, the syntax for the MERGE statement does not require the use of INTO. You simply use MERGE followed by the target table alias. This is a bit different from SQL standards where MERGE INTO is more common.
### Merge into syntax for ONLY INSERT NEW rows and avoid insert if exactly same row has been arrived from source. 
```sql
MERGE my_dataset.target_table AS t
USING my_dataset.temp_table AS s
ON t.id = s.id AND t.name = s.name AND t.value = s.value
WHEN NOT MATCHED THEN
  INSERT (id, name, value)
  VALUES (s.id, s.name, s.value)
```


##### If need to compare entire row between source and target (all columns) to check the records present or not in target , instead of comparing all column one by one we can use below:-
```SQL
MERGE my_dataset.target_table AS t
USING my_dataset.temp_table AS s
ON HASH(TO_JSON_STRING(t.*)) = HASH(TO_JSON_STRING(s.*))
WHEN NOT MATCHED THEN
  INSERT (column1, column2, ..., columnN)  -- List the columns you want to insert
  VALUES (s.column1, s.column2, ..., s.columnN)
```

- Make sure that your data types are compatible when using TO_JSON_STRING. Complex or nested data types might require additional handling.
- This method assumes that all columns are relevant for determining duplicates. If there are columns that shouldn't be considered (like timestamps), you may need to exclude them or adjust your approach accordingly.


#### Insert if new row (based on few key column comparision) and update if row already existing (based on key columns).
```sql
MERGE target_table AS t
USING source_table AS s
ON t.key_column1 = s.key_column1 AND t.key_column2 = s.key_column2
WHEN MATCHED THEN
    UPDATE SET 
        t.column_to_update1 = s.column_to_update1,
        t.column_to_update2 = s.column_to_update2
        -- Add more columns as needed
WHEN NOT MATCHED THEN
    INSERT (key_column1, key_column2, column_to_update1, column_to_update2)
    VALUES (s.key_column1, s.key_column2, s.column_to_update1, s.column_to_update2);
```
