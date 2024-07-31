<template>
  <div>
    <div class="header">
      <h1 style="font-size: 60px; font-family: '楷体'">剪刀石头布Game</h1>

      <el-button
        @click="makeChoice('剪刀')"
        type="primary"
        style="height: 40px; margin-left: 50px"
        >剪刀</el-button
      >
      <el-button @click="makeChoice('布')" type="primary" style="height: 40px"
        >布</el-button
      >
      <el-button @click="makeChoice('石头')" type="primary" style="height: 40px"
        >石头</el-button
      >
      <el-button
        @click="resetGame"
        size="medium"
        style="height: 40px; color: black; margin-left: 50px"
        >再来一局</el-button
      >
    </div>
    <div class="mainbox">
      <div class="column">
        <img src="@/img/左.png" alt="" />
        <span style="font-size: 60px; color: pink; font-family: '楷体'"
          >你的选择:
        </span>

        <img v-if="yourChoice == '布'" src="@/img/布.png" alt="" />
        <img v-else-if="yourChoice == '石头'" src="@/img/石头.png" alt="" />
        <img v-else-if="yourChoice == '剪刀'" src="@/img/剪刀.png" alt="" />
      </div>
      <div class="column">
        <span style="font-size: 60px; font-family: '楷体'"
          >结果: {{ result }}</span
        >
        <div>
          <span
            v-if="yourChoice == ''"
            style="
              position: absolute;
              font-size: 300px;
              font-family: '楷体';
              margin-top: 190px;
              margin-left: -150px;
            "
            >vs</span
          >
        </div>
      </div>
      <div class="column">
        <img v-if="computerChoice == '布'" src="@/img/布.png" alt="" />
        <img v-else-if="computerChoice == '石头'" src="@/img/石头.png" alt="" />
        <img v-else-if="computerChoice == '剪刀'" src="@/img/剪刀.png" alt="" />
        <span style="font-size: 60px; color: pink; font-family: '楷体'"
          >AI的选择:</span
        >
        <img src="@/img/右.png" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const yourChoice = ref('');
    const computerChoice = ref('');
    const result = ref(null);

    const choices = ['剪刀', '布', '石头'];

    function getRandomChoice() {
      const index = Math.floor(Math.random() * choices.length);
      return choices[index];
    }

    function determineWinner(yourChoice, computerChoice) {
      if (yourChoice === computerChoice) {
        return '平局!!!';
      } else if (
        (yourChoice === '剪刀' && computerChoice === '布') ||
        (yourChoice === '布' && computerChoice === '石头') ||
        (yourChoice === '石头' && computerChoice === '剪刀')
      ) {
        return '你赢了!!!';
      } else {
        return '你输了!!!';
      }
    }

    function makeChoice(choice) {
      yourChoice.value = choice;
      computerChoice.value = getRandomChoice();
      result.value = determineWinner(yourChoice.value, computerChoice.value);
    }

    function resetGame() {
      yourChoice.value = '';
      computerChoice.value = '';
      result.value = null;
    }

    return {
      yourChoice,
      computerChoice,
      result,
      makeChoice,
      resetGame,
    };
  },
};
</script>
<style>
.header {
  display: flex;
  justify-content: center;
  height: 100px;
  width: 100%;
  background-color: pink;
  align-items: center;
  /* background: url('../img/weather_bgc.png'); */
}
.bodyone {
  height: 200px;
  width: 100%;
  background-color: green;
}
.mainbox {
  display: flex;
  min-width: 1024px;
  max-width: 100%;
  height: 815px;
  margin: 0 auto;
  /* background-color: #fff; */
  background: url('../img/背景.jpg');
  padding: 10px 10px 0;
}

.mainbox .column {
  display: flex;
  width: 35%;
}
.mainbox .column:nth-child(1) {
  display: flex;
  align-items: center;
}
.mainbox .column:nth-child(3) {
  display: flex;
  align-items: center;
}
.mainbox .column:nth-child(2) {
  width: 30%;
}
.vs {
  width: 300px;
  height: 300px;
  display: flex;
  align-items: center;
}
</style>
