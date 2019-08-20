<template>
  <div class="full-calendar-header">
    <div class="header-left">
      <span class="prev-month" @click.stop="goPrev">{{leftArrow}} 上个月</span>
      <span class="title">{{title}}</span>
      <span class="next-month" @click.stop="goNext">下个月 {{rightArrow}}</span>
    </div>
  </div>
</template>
<script type="text/babel">
  import dateFunc from './dateFunc'
  import moment from 'moment';

  export default {
    props : {
      currentMonth : {},
      titleFormat  : {},
      firstDay     : {},
      monthNames   : {},
      locale       : {}
    },
    data () {
      return {
        leftArrow  : '<',
        rightArrow : '>'
      }
    },
    computed: {
      title () {
        if (!this.currentMonth) return;
        return this.currentMonth.locale(this.locale).format('YYYY年MM月')
      }
    },
    methods : {
      goPrev () {
        var newMonth = moment(this.currentMonth).subtract(1, 'months').startOf('month');
        this.$emit('change', newMonth);
      },
      goNext () {
        var newMonth = moment(this.currentMonth).add(1, 'months').startOf('month');
        this.$emit('change', newMonth);
      }
    }
  }
</script>
<style lang="scss">
.full-calendar-header{
  font-size: 12px;
  display: flex;
  align-items: center;
    .title{
      margin: 0 20px;
    }
    .prev-month,.next-month{
      cursor: pointer;
    }
}
</style>
