<template>
    <div class="main">
        <div class="view-topics" v-for="topic in topics" :key="topic.id">
        <div> <h3> {{topic.topicName}} </h3></div>
        <div> Due: {{dayNameAndTime(topic.topicDueDate)}}</div> 
        </div>
    </div>
</template>
<script>
import moment from 'moment';
import topicService from "../services/TopicService";
export default {
    name: 'view-topics',
    methods: {
        dayNameAndTime(date) {
          const getFullName = moment(date).format('MMM Do YY');
          return getFullName;
        }
    },
    data() {
        return {
            topics: [],
        };
    },
    created() {
        topicService.listTopics()
        .then((topicsData) => {
            this.topics = topicsData.data;
        
        })
        .catch((error) => {
            console.error(error + " all topics not able to be loaded");
        });
    }
    
}
</script>

<style>
.main {
   display: grid;
  grid-template-columns: 250px 250px 250px;
    
}
.view-topics{
  display: flex;
  flex-direction: column;
  align-items: center;
  border: 5px double rgb(9, 115, 148);
  margin: 10px;
  padding: 16px;
  border-radius: 10px;
}

</style>