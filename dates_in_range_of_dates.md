let now =new Date();
const recurr_type = "PID";

let after2Months = new Date();
after2Months.setMonth(after2Months.getMonth()+ 2)

// Returns an array of dates between the two dates
var getDates = function(startDate, endDate) {
  var dates = [],
      currentDate = startDate,
      addDays = function(days) {
        var date = new Date(this.valueOf());
        date.setDate(date.getDate() + days);
        return date;
      };
  while (currentDate <= endDate) {
    dates.push(currentDate);
    currentDate = addDays.call(currentDate, 1);
  }
  return dates;
};

// Usage
var dates = getDates(now, after2Months);                                                                                                           
dates.forEach(function(date) {
  console.log(date);
});
