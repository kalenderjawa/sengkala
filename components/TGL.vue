<template>
  <div class="tgl-container">
    <div class="cell cell-1">1</div>
    <div class="cell cell-2">2</div>
    <div class="cell cell-3">3</div>
    <div class="cell cell-4">4</div>
    <div class="cell cell-5">5</div>
    <div class="cell cell-6">6</div>
    <div class="cell cell-7">7</div>
    <div class="cell cell-8">8</div>
    <div class="cell cell-9">9</div>
    <div class="cell cell-4">10</div>
    <div class="cell cell-1">11</div>
    <div class="cell cell-2">12</div>
    <div class="cell cell-3">13</div>
    <div class="cell cell-4">14</div>
    <div class="cell cell-5">15</div>
    <div class="cell cell-6">16</div>
    <div class="cell cell-7">17</div>
    <div class="cell cell-8">18</div>
    <div class="cell cell-9">19</div>
    <div class="cell cell-1">20</div>
    <div class="cell cell-5">21</div>
    <div class="cell cell-2">22</div>
    <div class="cell cell-3">23</div>
    <div class="cell cell-4">24</div>
    <div class="cell cell-5">25</div>
    <div class="cell cell-6">26</div>
    <div class="cell cell-7">27</div>
    <div class="cell cell-8">28</div>
    <div class="cell cell-9">29</div>
    <div class="cell cell-1">30</div>
    <div class="cell cell-5">31</div>
  </div>
</template>

<script>
export default {
  name: 'TGL'
}
</script>

<style>
.tgl-container {
  height: 40vh;
  margin: 2rem;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr 1fr;
  grid-gap: 1px 1px;
}
.cell {
  color: white;
  font-size: 3rem;
  text-align: center;
  padding: 3rem;
}
.cell-1 {
  background: deepskyblue;
}
.cell-2 {
  background: orangered;
}
.cell-3 {
  background: royalblue;
}
.cell-4 {
  background: gold;
}
.cell-5 {
  background: blueviolet;
}
.cell-6 {
  background: limegreen;
}
.cell-7 {
  background: coral;
}
.cell-8 {
  background: lightseagreen;
}
.cell-9 {
  background: maroon;
}
</style>
