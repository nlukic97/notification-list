<template>
  <div class="hello">
    <ul>
        <li :class="{seen : notification.seen}" v-for="(notification, index) in notifications" v-bind:key="index"> <!-- ako je seen true, stavice klasu seen -->
          <div class="">
            <span class="circle" @click="markAsSeen(index)"></span>
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
  data(){
    return {
      notifications:[
        {
          title:'Elon Musk sent you a message',
          seen:false,
          timestamp: 1571106507
        },
        {
          title:'Mark Zuckeberg sent you a message',
          seen:false,
          timestamp: 1571106507
        },
        {
          title:'Milivoje would like to tag you in a photo',
          seen:false,
          timestamp: 1581106407
        },
        {
          title:'Radivoje liked your comment',
          seen:true,
          timestamp: 1590006507
        },
        {
          title:'CIA wants to know your location',
          seen:true,
          timestamp: 1491106507
        }
      ],
      dateSettings: {
        day: 'numeric', 
        month: 'long', 
        year:'numeric', 
        hour:'numeric',
        minute:'numeric'
        }
    }
  },
  methods: {
    markAsSeen: function(index){
      this.notifications[index].seen = true;
    },
    sortNotifications: function(){ //solution to displaying most recent - arr.sort(callback())
      this.notifications.sort(function(a,b){
        return b.timestamp - a.timestamp; //mixed this up originally
      })
    },
    displayHumanReadDate: function(){ //changing each individual array timestamp to human readable text
      for(var i = 0; i < this.notifications.length; i++){
        this.notifications[i].timestamp = new Date(this.notifications[i].timestamp * 1000).toLocaleString("en-US", this.dateSettings)
      }
    }
  },
  beforeMount(){ //pre nego sto se postavi sve, aktiviraj ovo da se sortira, jel to?
    this.sortNotifications();
    this.displayHumanReadDate();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  ul {
    list-style-type: none;
  }

  li {
    max-width: 550px;
    text-align: left;
    margin: 0 auto;
    background: rgb(43, 218, 209);
    line-height:50px;
  }

  li.seen {
    background-color:rgb(181, 236, 233);
  }
  li.seen .circle {
    background-color:rgb(126, 255, 126);
  }

  span {
    vertical-align: middle;
  }
  .circle {
    height:20px;
    width:20px;
    border-radius: 50%;
    background-color: lime;
    display:inline-block;
    margin: 0 10px;
  }
  .circle:hover {
    cursor: pointer;
  }

  .date {
    float:right;
    margin-right: 20px;
  }
  </style> 
