<template>
  <div class="waistline">
    <div class="back" @click="back">上一题</div>
    <h3>请输入您的腰围</h3>
    <div class="form">
      <input type="number" placeholder="请输入腰围" v-model="waistline" @input="inputFn"/>
      <strong>cm</strong>
      <button @click="confirm" :class="{ active: isActive }">确认</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      waistline: null,
      isActive: false,
    }
  },
  methods: {
    back() {
      this.$router.go(-1)
    },
    inputFn() {
      if (this.waistline) {
        this.isActive = true
      }else{
        this.isActive = false
      }
    },
    confirm() {
      if (this.waistline) {
        let user = JSON.parse(localStorage.getItem('userInfo'))
        let obj = { ...user, waistline: this.waistline / 1 }
        localStorage.setItem('userInfo', JSON.stringify(obj))
        this.$router.push('/result')
      }
    },
  },
}
</script>

<style lang="scss" scoped>
.waistline {
  h3 {
    margin-top: 60px;
    text-align: center;
    margin-bottom: 40px;
  }
  .form {
    text-align: center;
    input {
      width: 120px;
      height: 48px;
      border-radius: 20px;
      border: 3px solid black;
      font-weight: 600;
      font-size: 16px;
      padding: 5px;
      text-align: center;
      background-color: #f5f5f5;
      margin-right: 4px;
    }
  }
  button {
    width: 120px;
    height: 50px;
    border-radius: 20px;
    border: none;
    text-align: center;
    font-weight: 600;
    display: block;
    margin-left: auto;
    margin-right: auto;
    margin-top: 24px;
  }
  .active {
    background-color: #fdf052;
  }
}
</style>
