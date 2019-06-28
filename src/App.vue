<template>
  <div id="app">
    <div class="trees">
      <v-chart :options="options"></v-chart>
      <v-chart :options="options2"></v-chart>
    </div>
    <h1>{{current.name}}</h1>
    <div class="button">
      <button class="button" @click="dfs">Forward</button>
      <button class="button" @click="backwards">Backwards</button>
    </div>
  </div>
</template>

<script>
import ECharts from 'vue-echarts'
import "echarts/lib/chart/tree"
import "echarts/lib/component/tooltip"
import "echarts/lib/component/legend"
import "echarts/lib/component/title"

export default {
  name: 'app',
  components: {
    'v-chart': ECharts
  },
  data(){
    return{
      data: '',
      nodes: [],
      current: '',
      prev: '',
      count: 0,
      count2: 0, 
      reset: false,
      reset2: false,
      options: {
        label: {
          trigger: 'item',
          triggerOn: 'mousemove'
        },
        series: [{
          type: 'tree',
          data: [],
          left: '2%',
          right: '2%',
          top: '8%',
          bottom: '20%',
          symbol: 'circle',
          symbolSize: 20,
          orient: 'vertical',
          expandAndCollapse: false,
          label: {
              normal: {
                  position: 'top',
                  verticalAlign: 'middle',
                  align: 'middle',
                  fontSize: 20
              }
          },
          leaves: {
            label: {
              normal: {
                position: 'top',
                verticalAlign: 'middle',
                align: 'middle'
              }
            },
          },
        }]
      },
      options2: {
        label: {
          trigger: 'item',
          triggerOn: 'mousemove'
        },
        series: [{
          type: 'tree',
          data: [],
          left: '2%',
          right: '2%',
          top: '8%',
          bottom: '20%',
          symbol: 'circle',
          symbolSize: 20,
          orient: 'vertical',
          expandAndCollapse: false,
          label: {
              normal: {
                  position: 'top',
                  verticalAlign: 'middle',
                  align: 'middle',
                  fontSize: 20
              }
          },
          leaves: {
            label: {
              normal: {
                position: 'top',
                verticalAlign: 'middle',
                align: 'middle'
              }
            },
          },
        }]
      }
    }
  },
  mounted(){
    this.init()
    this.nodes = this.options2.series[0].data[0].children
    this.current = this.options.series[0].data[0]
    this.prev = this.options.series[0].data[0]
  },
  methods:{
    init(){
    let data = 
      {
        name: "Start",
        label: {          
        },
          itemStyle: {
            color: 'green',
            borderColor: 'green'
          },
        children: 
        [
          {
            name: Math.floor((Math.random() * 20) + 1),  
            value: Math.floor((Math.random() * 20) + 1),    
            label: {
              fontSize: 20
            },
            itemStyle: {
              color: '#f54542',
              borderColor: '#f54542'
            },
            children: [
              {
                name: Math.floor((Math.random() * 20) + 1),  
                value: Math.floor((Math.random() * 20) + 1),    
                label: {
                  fontSize: 20
                },
                itemStyle: {
                  color: '#f54542',
                  borderColor: '#f54542'
                },
                children: []
              },
            ]
          },
          {
            name: Math.floor((Math.random() * 20) + 1),  
            value: Math.floor((Math.random() * 20) + 1),    
            label: {
              fontSize: 20
            },
            itemStyle: {
              color: '#f54542',
              borderColor: '#f54542'
            },
            children: [
              {
                name: Math.floor((Math.random() * 20) + 1),  
                value: Math.floor((Math.random() * 20) + 1),    
                label: {
                  fontSize: 20
                },
                itemStyle: {
                  color: '#f54542',
                  borderColor: '#f54542'
                },
                children: []
              },
            ]
          },
          {
            name: Math.floor((Math.random() * 20) + 1),  
            value: Math.floor((Math.random() * 20) + 1),    
            label: {
              fontSize: 20
            },
            itemStyle: {
              color: '#f54542',
              borderColor: '#f54542'
            },
            children: [
              {
                name: Math.floor((Math.random() * 20) + 1),  
                value: Math.floor((Math.random() * 20) + 1),    
                label: {
                  fontSize: 20
                },
                itemStyle: {
                  color: '#f54542',
                  borderColor: '#f54542'
                },
                children: []
              },
            ]
          },
          {
            name: Math.floor((Math.random() * 20) + 1),  
            value: Math.floor((Math.random() * 20) + 1),    
            label: {
              fontSize: 20
            },
            itemStyle: {
              color: '#f54542',
              borderColor: '#f54542'
            },
            children: [
              {
                name: Math.floor((Math.random() * 20) + 1),  
                value: Math.floor((Math.random() * 20) + 1),    
                label: {
                  fontSize: 20
                },
                itemStyle: {
                  color: '#f54542',
                  borderColor: '#f54542'
                },
                children: []
              },
            ]
          },
        ]
      };
      for(let i=0; i<4; i++){
        data.children[i].children.push({
          name: Math.floor((Math.random() * 20) + 1),  
          value: Math.floor((Math.random() * 20) + 1),    
          label: {
            fontSize: 20
          },
          itemStyle: {
            color: '#f54542',
            borderColor: '#f54542'
          },
          children: []
        })
      }
      this.options.series[0].data.push(data)
      this.options2.series[0].data.push(data)
    },
    forward(){
      if(this.current.children.length > 0){
        this.prev = {...this.current}
        this.current = {...this.current.children[this.count]}
        this.current.itemStyle.borderColor = 'green'
        this.current.itemStyle.color = 'green'
      }
      else{
        this.current = {...this.prev}
        this.current.value=true
        this.count++
        this.current.itemStyle.borderColor = 'green'
        this.current.itemStyle.color = 'green'
      }
      if(this.prev.value == true && this.current.children.length > 0){
        this.count2++
        this.current = this.nodes[this.count2]
        this.prev = {...this.current}
        this.count = 0
        this.current.itemStyle.borderColor = 'green'
        this.current.itemStyle.color = 'green'
      }
    },
    backwards(){
      this.current = {...this.prev}
    },
    dfs(){
      if(this.nodes[this.count] != undefined && !this.reset){
        this.nodes[this.count].itemStyle.color = 'green'
        this.nodes[this.count].itemStyle.borderColor = 'green'
        this.count++
      }
      else{
        if(!this.reset){
          this.count = 0
          this.reset = true
        }
        if(this.nodes[this.count].children != undefined){
          if(this.nodes[this.count].children[this.count2] != undefined){
            this.nodes[this.count].children[this.count2].itemStyle.color = 'green'
            this.nodes[this.count].children[this.count2].itemStyle.borderColor = 'green'
            console.log({...this.nodes[this.count].children[this.count2]})
            this.count2++
          }
        else if(this.nodes[this.count+1].children[0] != undefined){
            this.count++
            if(!this.reset2){
              this.count2 = 0
              this.reset2 = false
            }
            this.nodes[this.count].children[this.count2].itemStyle.color = 'green'
            this.nodes[this.count].children[this.count2].itemStyle.borderColor = 'green'
            this.count2++
          }
        }
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

div.trees{
  display: flex;
}
</style>
