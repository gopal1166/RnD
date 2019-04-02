To fetch records that match today's timestamp

```
  $sql = "SELECT * FROM table WHERE  DATE('TIME_STAMP') = 'CURDATE()'";
```

To fetch records that mathes today and tomorrow timestamp

```
  $sql = "SELECT * FROM `planned_activity` WHERE DATE(`START_TIME`) = CURDATE() + interval 1 day OR DATE(`START_TIME`) = CURDATE()";
 ```
