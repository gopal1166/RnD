To fetch records that match today's timestamp

```
  $sql = "SELECT * FROM table WHERE  DATE('TIME_STAMP') = 'CURDATE()'";
```
