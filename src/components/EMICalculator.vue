<template>
  <div class="page-container">
    <br />
    <div id="loan-amount">
      <div class="flex-container">
        <div class="flex-items">
          Loan Amount
        </div>
        <div class="flexitem2 ">
          <input
            v-model="loanValue"
            class="input-box"
            min="0"
            @input="loanValue < 0 || isNaN(loanValue) ? (loanValue = 0) : ''"
          />

          <div class="item3">₹</div>
        </div>
      </div>
      <div id="slider" class="slider">
        <div class="slider-child">
          <input
            type="range"
            v-model.number="loanValue"
            class="input-range"
            min="0"
            max="20000000"
          />
          <div class="slider-scale">
            <div class="scale-format" style="left:0%">
              <div>|</div>
              <div>0</div>
            </div>
            <div class="scale-format" style="left:10%">
              <div style="margin-left:3px;">|</div>
              <div>25L</div>
            </div>
            <div class="scale-format" style="left:19%">
              <div style="margin-left:3px;">|</div>
              <div>50L</div>
            </div>
            <div class="scale-format" style="left:28%">
              <div style="margin-left:3px;">|</div>
              <div>75L</div>
            </div>
            <div class="scale-format" style="left:37%">
              <div style="margin-left:3px;">|</div>
              <div>100L</div>
            </div>
            <div class="scale-format" style="left:46%">
              <div style="margin-left:3px;">|</div>
              <div>125L</div>
            </div>
            <div class="scale-format" style="left:55%">
              <div style="margin-left:3px;">|</div>
              <div>150L</div>
            </div>
            <div class="scale-format" style="left:64%">
              <div style="margin-left:3px;">|</div>
              <div>175L</div>
            </div>
            <div class="scale-format" style="left:73%">
              <div style="margin-left:3px;">|</div>
              <div>200L</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div id="interest" style="margin-top:50px;">
      <div class="flex-container">
        <div class="flex-items">
          Interest
        </div>
        <div class="flexitem2 ">
          <input
            v-model="interest"
            @input="interest < 0 || isNaN(interest) ? (interest = 5) : ''"
            class="input-box"
            min="5"
          />
          <div class="item3">%</div>
        </div>
      </div>
      <div id="slider" class="slider">
        <div class="slider-child">
          <input
            type="range"
            v-model.number="interest"
            class="input-range"
            min="5.0"
            step="0.1"
            max="20.0"
          />
          <div class="slider-scale" style="margin-top:-3px;">
            <div class="scale-format">
              <div style="margin-left:3px;">|</div>
              <div>5</div>
            </div>
            <div class="scale-format" style="left:14%">
              <div style="margin-left:3px;">|</div>
              <div>7.5</div>
            </div>
            <div class="scale-format" style="left:27%">
              <div style="margin-left:3px;">|</div>
              <div>10</div>
            </div>
            <div class="scale-format" style="left:40%">
              <div style="margin-left:3px;">|</div>
              <div>12.5</div>
            </div>
            <div class="scale-format" style="left:53%">
              <div style="margin-left:3px;">|</div>
              <div>15</div>
            </div>
            <div class="scale-format" style="left:66%">
              <div style="margin-left:3px;">|</div>
              <div>17.5</div>
            </div>
            <div class="scale-format" style="left:80%">
              <div style="margin-left:3px;">|</div>
              <div>20</div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div id="loan-tenure" style="margin-top:50px;">
      <div class="flex-container">
        <div class="flex-items">
          Loan Tenure
        </div>
        <div class="flexitem2 ">
          <input
            v-model.number="year"
            class="input-box-tenure"
            min="1"
            @input="
              year < 0 || isNaN(year) ? (year = 1) : '', (month = year * 12)
            "
            v-if="tab === 'year'"
          />
          <input
            v-model.number="month"
            class="input-box-tenure"
            min="12"
            @input="month < 0 || isNaN(month) ? (month = 12) : ''"
            v-if="tab === 'month'"
          />

          <div class="item-tenure">
            <div
              class="btn1"
              id="year"
              :style="tab == 'year' ? 'background-color:#e9ecef' : ''"
              @click="(tab = 'year'), (year = month / 12)"
            >
              Yr
            </div>
            <div
              class="btn2"
              id="month"
              @click="(tab = 'month'), (month = year * 12)"
              :style="tab == 'month' ? 'background-color:#e9ecef' : ''"
            >
              Mo
            </div>
          </div>
        </div>
      </div>
      <div id="slider" class="slider">
        <div class="slider-child">
          <input
            type="range"
            v-model.number="year"
            class="input-range"
            min="0"
            max="30"
            v-if="tab === 'year'"
            @input="month = year * 12"
          />
          <input
            type="range"
            v-model.number="month"
            class="input-range"
            min="0"
            max="360"
            v-if="tab === 'month'"
          />
          <div class="slider-scale" style="margin-top:-3px;">
            <div class="scale-format">
              <div style="margin-left:3px;">|</div>
              <div>0</div>
            </div>
            <div class="scale-format" style="left:14%">
              <div style="margin-left:3px;">|</div>
              <div>{{ tab === "year" ? 5 : 60 }}</div>
            </div>
            <div class="scale-format" style="left:27%">
              <div style="margin-left:3px;">|</div>
              <div>{{ tab === "year" ? 10 : 120 }}</div>
            </div>
            <div class="scale-format" style="left:40%">
              <div style="margin-left:3px;">|</div>
              <div>{{ tab === "year" ? 15 : 180 }}</div>
            </div>
            <div class="scale-format" style="left:53%">
              <div style="margin-left:3px;">|</div>
              <div>{{ tab === "year" ? 20 : 240 }}</div>
            </div>
            <div class="scale-format" style="left:66%">
              <div style="margin-left:3px;">|</div>
              <div>{{ tab === "year" ? 25 : 300 }}</div>
            </div>
            <div class="scale-format" style="left:80%">
              <div style="margin-left:3px;">|</div>
              <div>{{ tab === "year" ? 30 : 360 }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div id="showCalculatedData" class="showData">
      <div class="numericData" style="text-align: center">
        <div id="EMI" style="display: flex;flex-direction:column;">
          <div>EMI of Loan</div>
          <div>
            {{ displayEMI > 0 ? rupeeFormat(Math.round(displayEMI)) : 0 }}
          </div>
        </div>
        <div
          id="total-interest"
          style="display: flex;flex-direction:column;margin-top:20px;"
        >
          <div style="">Total Interest Payable</div>
          <div>
            {{
              displayEMI > 0
                ? month
                  ? rupeeFormat(Math.round(displayEMI * month - loanValue))
                  : rupeeFormat(Math.round(displayEMI * year * 12 - loanValue))
                : 0
            }}
          </div>
        </div>
        <div
          id="total-payable-amout"
          style="display: flex;flex-direction:column;margin-top:20px;"
        >
          <div style="">Total Payable Amount</div>
          <div>
            {{
              displayEMI > 0
                ? month
                  ? rupeeFormat(Math.round(displayEMI * month))
                  : rupeeFormat(Math.round(displayEMI * year * 12))
                : 0
            }}
          </div>
        </div>
      </div>
      <div style="width:50%;" class="graphData">
        <GoogleChart
          :totalAmount="
            month
              ? Math.round(displayEMI * month)
              : Math.round(displayEMI * year * 12)
          "
          :totalInterest="
            month
              ? Math.round(displayEMI * month - loanValue)
              : Math.round(displayEMI * year * 12 - loanValue)
          "
        />
      </div>
    </div>
    <div class="table-container">
      <table>
        <tr>
          <th style="width:10%; background: #dedede">Year</th>
          <th style="background: #88a825;color:white;width:15%">Principal</th>
          <th style="background: #ed8c2b;color:white;width:15%">Interest</th>
          <th style="background: #dedede;width:20%">Total Payments</th>
          <th style="background:#b8204c;color:white;width:30%">Balance</th>
          <th>Loan Paid to Date</th>
        </tr>
        <tr v-for="index in month" :key="currentYear + index - 1">
          <td style="width:5%">
            {{ displayMonth(index, currentMonth) }}
          </td>
          <td style="width:15%">
            ₹ {{ rupeeFormat(displayPrincipal(month - index + 1, displayEMI)) }}
          </td>
          <td style="width:15%">
            ₹
            {{
              rupeeFormat(
                Math.round(displayEMI) -
                  displayPrincipal(month - index + 1, displayEMI)
              )
            }}
          </td>
          <td style="width:20%">
            ₹
            {{ rupeeFormat(Math.round(displayEMI)) }}
          </td>
          <td style="width:15%">
            ₹
            <!-- This Calculation for total balance-->
            <!-- {{
              rupeeFormat(
                displayBalance(displayPrincipal(month - index + 1, displayEMI))
              )
            }} -->
          </td>
          <td style="width:15%">
            <!-- {{ displayPaidPercentage() }} -->
            %
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import GoogleChart from "./GoogleChart.vue";
export default {
  name: "SliderInput",
  data() {
    return {
      monthNames: [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sept",
        "Oct",
        "Nov",
        "Dec",
      ],
      prevAmount: "",
      principal: "",
      loanValue: 0,
      interest: 5,
      year: 0,
      month: 0,
      tab: "year",
      currentYear: "",
      currentMonth: "",
    };
  },
  components: {
    GoogleChart,
  },
  created() {
    const current = new Date();
    const year = `${current.getFullYear()}`;
    this.currentMonth = parseInt(`${current.getMonth()}`);
    this.currentYear = parseInt(year);
  },
  computed: {
    displayEMI() {
      const rate = this.interest / 1200;
      if (this.year > 0) {
        const rn = rate + 1;
        const duration = this.year * 12;
        const val = Math.pow(rn, duration);
        const EMI = (this.loanValue * rate * val) / (val - 1);
        return EMI > 0 ? EMI : 0;
      } else {
        const rn = rate + 1;
        const val = Math.pow(rn, this.month);
        const EMI = (this.loanValue * rate * val) / (val - 1);
        return EMI > 0 ? EMI : 0;
      }
    },
  },
  methods: {
    rupeeFormat(val) {
      const data = val.toString();
      let lastThree = data.substring(data.length - 3);
      let otherNumbers = data.substring(0, data.length - 3);
      if (otherNumbers != "") lastThree = "," + lastThree;
      return otherNumbers.replace(/\B(?=(\d{2})+(?!\d))/g, ",") + lastThree;
    },
    displayMonth(index, month) {
      if (month + index - 1 > 12) {
        return this.monthNames[(month + index - 1) % 12];
      }
      if (month + index - 1 == 12) {
        return this.monthNames[0];
      } else {
        return this.monthNames[month + index - 1];
      }
    },
    displayPrincipal(n, EMI) {
      const rate = this.interest / 1200;
      const rn = rate + 1;
      const val = Math.pow(rn, n);
      return Math.round(EMI / val) > 0 ? Math.round(EMI / val) : "";
    },
    displayBalance(principal) {
      if (this.prevAmount > 0) {
        this.prevAmount = this.prevAmount - principal;
        return this.prevAmount < 0 ? 0 : this.prevAmount;
      } else {
        this.prevAmount = this.loanValue - principal;
        return this.prevAmount < 0 ? 0 : this.prevAmount;
      }
    },
    displayPaidPercentage() {
      return Math.round(100 - (this.prevAmount / this.loanValue) * 100);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.showData {
  justify-content: center;
}
.numericData {
  display: flex;
  flex-direction: column;
  width: 50%;
}
.table-container {
  display: flex;
  justify-content: center;
  width: 100%;
  margin-top: 50px;
}
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}
.showData {
  margin-top: 50px;
}
th {
  border: 1px solid #dddddd;
  text-align: center;
  padding: 8px;
  height: 50px;
}
td {
  border: 1px solid #dddddd;
  text-align: right;
  padding: 8px;
}
@media (min-width: 200px) and (max-width: 500px) {
  .page-container {
    width: 504px;
    align-items: center;
    margin: 0px;
  }
  .graphData {
    text-align: center;
    margin-top: 50px;
  }
  .numericData {
    margin-left: 10%;
    font-size: 20px;
    color: #333;
    font-weight: bold;
  }
  .flex-items {
    align-items: center;
    font-size: 1.5em;
    margin-top: 2px;
    margin-left: 25px;
    width: 150px;
  }
  .input-box {
    width: 40%;
  }
  .input-box-tenure {
    width: 40%;
  }
  .scale-format {
    position: relative;
    font-size: 8px;
    color: #333;
    margin-top: -8px;
    display: flex;
    flex-direction: column;
    width: 11px;
  }
  .slider-child {
    justify-content: center;
    align-items: center;
    width: 85%;
  }
  .table-container {
    width: 90%;
  }
}
@media (min-width: 500px) and (max-width: 780px) {
  .page-container {
    width: 945px;
    align-items: center;
    margin: 0px;
  }
  .numericData {
    margin-left: 10%;
    font-size: 20px;
    color: #333;
    font-weight: bold;
  }
  .graphData {
    text-align: center;
    margin-top: 50px;
    margin-left: 10%;
  }
  .input-box {
    width: 40%;
  }
  .input-box-tenure {
    width: 40%;
  }
  .flex-container {
    display: flex;
    flex-wrap: wrap;
    margin-left: 5%;
    width: 100%;
  }
  .scale-format {
    position: relative;
    font-size: 10px;
    color: #333;
    margin-top: -8px;
    display: flex;
    flex-direction: column;
    width: 22px;
  }
  .slider-child {
    justify-content: center;
    align-items: center;
    width: 91%;
  }
  .table-container {
    width: 90%;
  }
}
@media (min-width: 780px) {
  .page-container {
    width: 1260px;
    align-items: center;
    margin: auto;
  }
  .numericData {
    font-size: 20px;
    color: #333;
    font-weight: bold;
  }
  .input-box {
    width: 70%;
  }
  .input-box-tenure {
    width: 70%;
  }
  .flex-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    width: 100%;
  }
  .showData {
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    align-items: center;
    justify-content: center;
  }
  .scale-format {
    position: relative;
    font-size: 12px;
    color: #333;
    margin-top: -8px;
    display: flex;
    flex-direction: column;
    width: 30px;
  }
  .slider {
    margin-left: 3%;
  }
  .slider-child {
    justify-content: center;
    align-items: center;
    width: 91%;
  }
  .table-container {
    width: 90%;
  }
}
.slider-scale {
  display: flex;
  flex-direction: row;
  margin-top: 0px;
  flex-wrap: nowrap;
}
.input-range {
  width: 100%;
}
.slider {
  margin-top: 30px;
  width: 80%;
}
.flex-items {
  align-items: center;
  font-size: 1.5em;
  margin-top: 2px;
  width: 150px;
}
.flexitem2 {
  width: 500px;
  margin-left: 20px;
  display: flex;
  flex-direction: row;
}
.input-box {
  border-radius: 0.25em 0 0 0.25em;
  padding: 0.5rem 0.75rem;
  border: 1px solid #ced4da;
}
.item3 {
  padding: 0.6rem 0.75rem;
  border-radius: 0 0.25em 0.25em 0;
  background-color: #e9ecef;
  border: 1px solid #ced4da;
  width: 5%;
}
.input-box-tenure {
  border-radius: 0.25em 0 0 0.25em;
  padding: 0.5rem 0.75rem;
  border: 1px solid #ced4da;
}
.item-tenure {
  border-radius: 0 0.25em 0.25em 0;
  width: 11%;
  display: flex;
}
.btn1 {
  padding: 0.6rem 0.75rem;
  border: 1px solid #ced4da;
  display: block;
  width: 100%;
  cursor: pointer;
}
.btn2 {
  border-radius: 0 0.25em 0.25em 0;
  padding: 0.6rem 0.75rem;
  border: 1px solid #ced4da;
  display: block;
  width: 100%;
  cursor: pointer;
}
</style>
