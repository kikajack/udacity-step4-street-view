<template>
	<div id="map-container">
		<div id="header"></div>
		<div id="map"></div>
		<div id="select" class="select select-show">
			<div class="select-content">
				<select class="change-type" v-model="selected">
          <option disabled value="">请选择</option>
          <option v-for="option in options" v-bind:value="option.value">
            {{ option.text }}
          </option>
					<!-- <option disabled value="all">全部</option>
					<option value="hospital">医院</option>
					<option value="bank">银行</option>
					<option value="market">商场</option> -->
				</select>
				<ul id="area-list" class="area-list">
					<li v-for="area in areas">
            <a @click=selectArea">{{ area }}</a>
          </li>
				</ul>
			</div>
			<div class="select-button">
				<a href="#" class="nav-toggle" v-on:click="toggleSelect"></a>
			</div>
		</div>
	</div>
</template>

<script type="text/javascript">
export default {
  name: 'Map',
  data () {
    return {
      selected: '',
      options: [
        { text: '医院', value: '医院' },
        { text: '银行', value: '银行' },
        { text: '商场', value: '商场' }
      ],
      areas: ''
    }
  },
  methods: {
    toggleSelect: function (val) {
      var select_div = document.getElementById('select')
      if (select_div.classList.contains('select-show')) {
          select_div.classList.remove('select-show')
      } else {
          select_div.classList.add('select-show')
      }
    },
    areasChange: function () {
        var local = new BMap.LocalSearch(map, {
          renderOptions:{map: map, autoViewport:true, panel:"area-list"},
          pageCapacity: 8
        })
        local.search(this.selected)
    }
  },
  watch: {
    selected: function () {
      this.areasChange(this.selected)
    }
  }
}
</script>

<style type="text/css">
#map-container {
  width: 100%;
  height: 100%;
}
#header {
	width: 100%;
	height: 6rem;
	background-color: #444;
}
#map {
  position: absolute!important;
	width: 100%;
	height: calc(100% - 6rem);
}
#select {
	position: absolute;
	top: 0px;
	left: -20rem;
	height: 100%;
	width: 30rem;
}
#select.select-show {
	left: 0px;
}
.select-content {
	float: left;
	width: 20rem;
	height: 100%;
	background-color: #000;
}
.change-type {
	width: 16rem;
	height: 2rem;
	margin: 2rem;
}
.area-list {
	margin: 0.2rem;
	background-color: #eee;
  list-s tyle: none;
}
.area-list li {
	margin-top: 2rem;
}
.select-button {
	float: left;
	width: 6rem;
	height: 6rem;
	background-color: red;
}
.select-button a {
	position: relative;
	width: 100%;
}
.select-show .select-content {
	
}
.select-show .select-button {

}
.nav-toggle:before {
    color: #fff;
    font-family: "responsivenav", sans-serif;
    font-style: normal;
    font-weight: normal;
    font-variant: normal;
    font-size: 6rem;
    text-transform: none;
    position: absolute;
    content: "≡";
    text-indent: 0;
    text-align: center;
    line-height: 5.5rem;
    speak: none;
    width: 100%;
    top: 0;
    left: -1.5rem;
}
</style>