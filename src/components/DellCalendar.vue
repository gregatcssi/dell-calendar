

<template>
<div>
<table class="col-xs-12">
  <caption><h2>{{CurrentMonth.MonthName}}</h2>  </caption>
    <thead>
      <th style="color: rgb(0, 125, 184) ;">QW</th>
      <th style="color: rgb(0, 125, 184) ;">W</th>
      <th>Sa</th>
      <th>Su</th>
      <th>Mo</th>
      <th>Tu</th>
      <th>We</th>
      <th>Th</th>
      <th>Fr</th>
    </thead>
    <tbody v-for="week in CurrentMonth.MonthDates">
      <week :WeekInformation=week />
    </tbody>
  </table>





<!-- <div v-for="Month in theMonths">
    <h2>{{Month.MonthName}}</h2>
<table class="col-xs-12">
      <thead>
        <th style="color: rgb(0, 125, 184) ;">QW</th>
        <th style="color: rgb(0, 125, 184) ;">W</th>
        <th>Sa</th>
        <th>Su</th>
        <th>Mo</th>
        <th>Tu</th>
        <th>We</th>
        <th>Th</th>
        <th>Fr</th>
      </thead>
      <tbody v-for="week in Month.weeks">
        <week :WeekInformation=week />
          </tbody></table>




</div>-->
</div>


</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { ArrayPropsDefinition } from "vue/types/options";
import week from "./week.vue";

@Component({
  components: { week }
})
export default class DellCalendar extends Vue {
  @Prop() private fiscalYear!: string;
  startDate!: string;
  endDate!: string;
  theDates = [];
  theWeeks = [];
  theMonths = [];
  CurrentMonth = {};
  start: Date;
  end: Date;
  fisYear: number;

  constructor() {
    super();
    console.log(this.startDate);
    console.log(this.endDate);

    // this.startDate = "2/3/2018";
    // this.endDate = "2/1/2019";
    this.fisYear = 2019;
    this.start = new Date(this.startDate);
    this.end = new Date(this.endDate);
    setTimeout(() => this.generateDates(), 50);
    //setTimeout(  this.generateDates(),100000);
  }

  generateDates() {
    console.log("Go");
    if (!this.theWeeks) {
      this.theWeeks = [];
    }
    if (!this.theDates) {
      this.theDates = [];
    }
    if (!this.theMonths) {
      this.theMonths = [];
    }
    let UseThisWeek = 0;
    let startAndEndDates = [
      {
        fisYear: 2019,
        startDate: new Date("2/3/2018"),
        endDate: new Date("2/1/2019")
      },
      {
        fisYear: 2020,
        startDate: new Date("2/2/2019"),
        endDate: new Date("1/31/2020")
      },
      {
        fisYear: 2021,
        startDate: new Date("2/1/2020"),
        endDate: new Date("1/30/2021")
      }
    ];
    let today = new Date(Date.now());
    let startDate = new Date();
    let endDate = new Date();
    startAndEndDates.forEach(dt => {
      if (dt.startDate <= today && dt.endDate > today) {
        startDate = dt.startDate;
        endDate = dt.endDate;
        this.fisYear = dt.fisYear;
      }
    });
    let Incr = 0;
    let QIncr = 1;
    let WIncr = 1;
    let week = [];
    let d = today.getDate();
    let m = today.getMonth();
    let y = today.getFullYear();
    let td = d + "/" + m + "/" + y;
    let thisMonth = false;
    for (let day = startDate; day <= endDate; day.setDate(day.getDate() + 1)) {
      Incr++;
      let dd = day.getDate();
      let md = day.getMonth();
      let yd = day.getFullYear();
      let tdd = dd + "/" + md + "/" + yd;
      if (tdd === td) {
        let tmp = { d: day.getDate(), c: "rgb(25, 0, 255)" };
        week.push(tmp);
        thisMonth = true;
      } else {
        let tmp = { d: day.getDate(), c: "rgb(49, 49, 49)" };
        week.push(tmp);
      }
      if (Incr % 7 === 0) {
        if (thisMonth) {
          UseThisWeek = WIncr;
        }
        thisMonth = false;
        if (QIncr >= 14) {
          QIncr = 1;
        }
        let tmpweekhr = { W: WIncr, Q: QIncr };
        this.theWeeks.push(tmpweekhr);
        QIncr++;
        WIncr++;
        if (QIncr === 5) {
          week[6].c = "rgb(218,150,148)";
        } else if (QIncr === 10) {
          week[6].c = "rgb(33,89,103)";
        } else if (QIncr === 11) {
          week[6].c = "rgb(196,215,155)";
        }
        this.theDates.push({ weekinfo: tmpweekhr, weekDates: week });
        week = [];
      }
    }

    let jan = [];
    let feb = [];
    let mar = [];
    let apr = [];
    let may = [];
    let jun = [];
    let jul = [];
    let aug = [];
    let sept = [];
    let oct = [];
    let nov = [];
    let dec = [];
    this.theDates.forEach((week, index) => {
      if (index >= 0 && index < 4) {
        feb.push(week);
      } else if (index >= 4 && index < 8) {
        mar.push(week);
      } else if (index >= 8 && index < 13) {
        apr.push(week);
      }
      if (index >= 13 && index < 17) {
        may.push(week);
      } else if (index >= 17 && index < 21) {
        jun.push(week);
      } else if (index >= 21 && index < 26) {
        jul.push(week);
      } else if (index >= 26 && index < 30) {
        aug.push(week);
      } else if (index >= 30 && index < 34) {
        sept.push(week);
      } else if (index >= 34 && index < 39) {
        oct.push(week);
      } else if (index >= 39 && index < 43) {
        nov.push(week);
      } else if (index >= 43 && index < 47) {
        dec.push(week);
      } else if (index >= 47 && index < 52) {
        jan.push(week);
      }
    });
    UseThisWeek = UseThisWeek - 1;
    if (UseThisWeek >= 0 && UseThisWeek < 4) {
      this.CurrentMonth = { MonthName: "February", MonthDates: feb };
    } else if (UseThisWeek >= 4 && UseThisWeek < 8) {
      this.CurrentMonth = { MonthName: "March", MonthDates: mar };
    } else if (UseThisWeek >= 8 && UseThisWeek < 13) {
      this.CurrentMonth = { MonthName: "April", MonthDates: apr };
    } else if (UseThisWeek >= 13 && UseThisWeek < 17) {
      this.CurrentMonth = { MonthName: "May", MonthDates: may };
    } else if (UseThisWeek >= 17 && UseThisWeek < 21) {
      this.CurrentMonth = { MonthName: "June", MonthDates: jun };
    } else if (UseThisWeek >= 21 && UseThisWeek < 26) {
      this.CurrentMonth = { MonthName: "July", MonthDates: jul };
    } else if (UseThisWeek >= 26 && UseThisWeek < 30) {
      this.CurrentMonth = { MonthName: "August", MonthDates: aug };
    } else if (UseThisWeek >= 30 && UseThisWeek < 34) {
      this.CurrentMonth = { MonthName: "September", MonthDates: sept };
    } else if (UseThisWeek >= 34 && UseThisWeek < 39) {
      this.CurrentMonth = { MonthName: "October", MonthDates: oct };
    } else if (UseThisWeek >= 39 && UseThisWeek < 43) {
      this.CurrentMonth = { MonthName: "November", MonthDates: nov };
    } else if (UseThisWeek >= 43 && UseThisWeek < 47) {
      this.CurrentMonth = { MonthName: "December", MonthDates: dec };
    } else if (UseThisWeek >= 47 && UseThisWeek < 52) {
      this.CurrentMonth = { MonthName: "January", MonthDates: jan };
    }
    this.theMonths.push({ MonthName: "February", weeks: feb });
    this.theMonths.push({ MonthName: "March", weeks: mar });
    this.theMonths.push({ MonthName: "April", weeks: apr });
    this.theMonths.push({ MonthName: "May", weeks: may });
    this.theMonths.push({ MonthName: "June", weeks: jun });
    this.theMonths.push({ MonthName: "July", weeks: jul });
    this.theMonths.push({ MonthName: "August", weeks: aug });
    this.theMonths.push({ MonthName: "September", weeks: sept });
    this.theMonths.push({ MonthName: "October", weeks: oct });
    this.theMonths.push({ MonthName: "November", weeks: nov });
    this.theMonths.push({ MonthName: "December", weeks: dec });
    this.theMonths.push({ MonthName: "January", weeks: jan });
    console.log(this.CurrentMonth);
  }
  getcurrentMonth() {
    this.theMonths;
  }
}
</script>


<style scoped>
td,
th {
  background-color: rgb(49, 49, 49);
  text-align: center;
  padding: 3px;
  color: aliceblue;
  border: rgb(49, 49, 49) solid;
  border-radius: 15px;
}

table {
  padding-bottom: 15px;
}
</style>




