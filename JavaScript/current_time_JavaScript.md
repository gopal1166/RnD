To return current time object in format: 'YY-MM-DD HH:MM'

```
  getCurrentDateTime() {
    var now = new Date(),
      month = '' + (now.getMonth() + 1),
      day = '' + now.getDate(),
      year = now.getFullYear(),
      hours = '' + now.getHours(),
      minutes = '' + now.getMinutes();

    if (month.length < 2) month = '0' + month;
    if (day.length < 2) day = '0' + day;
    if (hours.length < 2) hours = '0' + hours;
    if (minutes.length < 2) minutes = '0' + minutes;


    var currentDate = [year, month, day].join('-');
    var currentTime = [hours, minutes].join(':');
    var dateTime = currentDate + ' ' + currentTime;
    return dateTime;
  }
  ```
