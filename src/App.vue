<template>
  <div id="app">
    <h1>Visualisation of Depth First and Breadth First search</h1>
    <div class="trees">
      <v-chart :options="options"></v-chart>
      <v-chart :options="options2"></v-chart>
    </div>

    <div class="buttons">
      <button class="button" @click="dfs">Travel bfs</button>
      <button class="button" @click="bfs">Travel BFS</button>
      <button class="button" @click="travel">Travel</button>
    </div>

    <div class="current">
      <h1 class="num">{{current.name}}</h1>
      <h1 class="num">{{currentBFS.name}}</h1>
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

      currentBFS: '',
      nodesBFS: [],
      prevBFS: '',
      countBFS: 0,
      count2BFS: 0, 
      resetBFS: false,
      reset2BFS: false,
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
    this.nodes = this.options.series[0].data[0].children
    this.current = this.options.series[0].data[0]
    this.prev = this.options.series[0].data[0]

    this.initBFS()
    this.nodesBFS = this.options2.series[0].data[0].children
    this.currentBFS = this.options2.series[0].data[0]
    this.prevBFS = this.options2.series[0].data[0]
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
      this.options.series[0].data = [...this.options.series[0].data, data]
    },

    initBFS(){
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

      this.options2.series[0].data = [...this.options2.series[0].data, data]
    },

    travel(){
      this.dfs()
      this.bfs()
    },

    dfs(){
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
    bfs(){
      if(this.nodesBFS[this.countBFS] != undefined && !this.resetBFS){
        this.nodesBFS[this.countBFS].itemStyle.color = 'green'
        this.nodesBFS[this.countBFS].itemStyle.borderColor = 'green'
        this.currentBFS = this.nodesBFS[this.countBFS]
        this.countBFS++
      }
      else{
        if(!this.resetBFS){
          this.countBFS = 0
          this.resetBFS = true
        }
        if(this.nodesBFS[this.countBFS].children != undefined){
          if(this.nodesBFS[this.countBFS].children[this.count2BFS] != undefined){
            this.nodesBFS[this.countBFS].children[this.count2BFS].itemStyle.color = 'green'
            this.nodesBFS[this.countBFS].children[this.count2BFS].itemStyle.borderColor = 'green'
            this.currentBFS = this.nodesBFS[this.countBFS].children[this.count2BFS]
            this.count2BFS++
          }
        else if(this.nodesBFS[this.countBFS+1].children[0] != undefined){
            this.countBFS++
            if(!this.reset2BFS){
              this.count2BFS = 0
              this.reset2BFS = false
            }
            this.nodesBFS[this.countBFS].children[this.count2BFS].itemStyle.color = 'green'
            this.nodesBFS[this.countBFS].children[this.count2BFS].itemStyle.borderColor = 'green'
            this.currentBFS = this.nodesBFS[this.countBFS].children[this.count2BFS]
            this.count2BFS++
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

  display: table;
  margin: 0 auto;
}

div.trees{
  margin-top: 120px;
  display: flex;
}

div.buttons{
  margin: 2rem;
}

div.current{
  display: flex;
  margin: 2rem;
}

button.button{
  margin-left: 10rem;
  margin-right: 10rem;
}

.num{
  width: 80px;
  margin-left: 18rem;
  margin-right: 8rem;
}
</style>
