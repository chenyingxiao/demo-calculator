<template>
    <div class="container-fluid bg-light">
        <div class="row">
            <div class="col-9 main-right">
                <div class="row input-01" v-text="equation"></div>
                <div class="row input-02" v-text="result"></div>
                <div class="d-flex btn-row flex-wrap">
                    <div class="text-center d-flex flex-column justify-content-center iconfont btn-item"
                         v-for="item in btnTextList"
                         v-html="item"
                         @click="btnClick(item)"></div>
                </div>
            </div>
            <div class="col-3"></div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      btnTextList: ['%', 'CE', 'C', '&#xe627;', '1/x', 'x*x', '2√', '/', '7', '8', '9', '*',
                    '4', '5', '6', '-', '1', '2', '3', '+', '+/-', '0', '.', '='],
      firstNum: '',
      twoNum: '',
      symbol: '',
      result: 0,
      equation: ''
    }
  },
  methods: {
    btnClick (val) {
      if('0123456789.'.indexOf(val) == -1){
        if (val === '=') {
          if (!this.twoNum){
            this.twoNum = this.result
          }
          this.equation = this.firstNum + this.symbol + this.twoNum + val
          this.result = eval(this.firstNum + this.symbol + this.twoNum)
          this.firstNum = this.twoNum = this.symbol = ''
          return
        }
        this.symbol = val
        this.equation = this.firstNum + this.symbol
      } else {
        if(this.symbol){
          this.result = this.twoNum += val
        } else {
          this.result = this.firstNum += val
          this.equation = ''
        }
      }

    }
  }
}
</script>

<style scoped>
    @import "../assets/css/iconfont.css";
    .input-01,
    .input-02{
        display: flex;
        justify-content: flex-end;
        align-items: center;
        height: 5rem;
        width: 100%;
    }
    .btn-item{
        width: 25%;
        height: 5rem;
        background-color: #fff;
        box-sizing: border-box;
        border: 1px solid #f8f9fa;
        font-size: 1.4rem;
    }
    .btn-item:hover{
        background-color: #ccc;
        cursor: pointer;
    }
    .main-right{
        border-right: 1px solid #ccc;
        padding: 0;
    }
</style>