<template>
  <div class="hello">
    <ul>
      <li :class="{'seen':notification.seen}" v-for="(notification, index) in notifications" v-bind:key="index">
        <div class="">
          <span v-on:click="markAsSeen(index)" class="circle"></span>
          <span>{{notification.title}}</span>
           <span class="date">{{notification.timestamp}}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      notifications:[
        {
          title:"Elon Musk sent you a message" ,
          seen:true ,
          timestamp: 1591106510
        },
        { 
          title:"Mark Zuckerbeg sent you a message" ,
          seen:false ,
          timestamp: 1281106505
        },
        { 
          title:"Milivoje would like to tag you in a photo" ,
          seen:false ,
          timestamp: 1361106303
        },
        { 
          title:"Radivoje liked your comment" ,
          seen:true ,
          timestamp: 1331106300
        },
        { 
          title:"BIA wants to know your location" ,
          seen:true ,
          timestamp: 1291106265
        }
      ],

       dateSettings: {
        hour:'numeric',
        minute:'numeric'
        }
    }
  },
  methods: {
    markAsSeen: function(index){
      this.notifications[index].seen = true;
    },
    sortNotifications: function(){
      this.notifications.sort(function(a,b){
        return b.timestamp - a.timestamp; 
      })
    },
    displayHumanReadDate: function(){ 
      for(var i = 0; i < this.notifications.length; i++){
        this.notifications[i].timestamp = new Date(this.notifications[i].timestamp * 1000).toLocaleString("en-US", this.dateSettings)
      }
    }
  },
  beforeMount(){    this.sortNotifications();
    this.displayHumanReadDate();
  }
}
 

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul{
  list-style:none;

}

li{
  max-width: 550px;
  text-align:left;
  margin:0 auto;
  background:rgb(21, 219, 209);
  line-height: 50px;

}

li.seen{
  background:rgb(156, 235, 231);
}

span{
  vertical-align:middle;


}

.circle{
  height:20px;
  width:20px;
  border-radius:50%;
  background-color: rgb(0, 255, 0);
  display:inline-block;
  margin: 0 10px;
  cursor: pointer;
}

li.seen.circle{
  background: rgb(118, 216, 118);
}

.date{
  float:right;
  margin-right: 15px;
}



</style>
