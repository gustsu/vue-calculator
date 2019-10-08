<template>
  <div class="calculator threed">
    <div class="display">{{ current || "0" }}</div>
    <div @click="clear" class="btn operator top-operator">C</div>
    <div @click="sign" class="btn operator top-operator">+/-</div>
    <div @click="percent" class="btn operator top-operator">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="append('0')" class="btn zero">00</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator equals">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }
};
</script>

<style lang="scss" scoped>
$red: #ea6262;
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 22px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  background: #fff;
  border-radius: 20px;
  box-shadow: 0 8px 40px rgba(0, 0, 0, 0.25);
  padding: 30px;
  color: #343434;
  overflow: hidden;
}

.calculator.threed {
  transform: rotateX(65deg) rotateZ(-35deg);
}

.btn {
  display: block;
  flex: 0 0 60px;
  height: 60px;
  line-height: 60px;
  margin: 20px;
  background: #fff;
  border-radius: 100%;
  cursor: pointer;
}
.btn:hover,
.btn:active {
  background: #ccc;
}

.btn.operator:hover,
.btn.operator:active {
  background: #ccc;
}

.display {
  flex: 0 0 100%;
  color: #333;
  text-align: right;
  font-size: 78px;
  padding: 100px 0px 15px;
  border-bottom: 1px solid #dedede;
  margin-bottom: 15px;
}

.operator {
  background: #f0f0f0;
  color: $red;
  font-size: 24px;
}

.btn.operator.top-operator {
  color: #343434;
}
.btn.operator.equals {
  background: $red;
  color: #fff;
}
.btn.operator.equals:hover,
.btn.operator.equals:active {
  background: darken($red, 10%);
}
</style>
