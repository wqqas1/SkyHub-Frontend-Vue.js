/**
 * Created by Alexandru Ionut Budisteanu - SkyHub on 6/21/2017.
 * (C) BIT TECHNOLOGIES
 */



/*
 PreviewTopic can also work with a prop id="1_frm_3333", and it fetch automatically the forum from you
 */


<template>
    <div>

       <ViewReply
              v-for="(reply, index) in getChildReplies"
              :reply="reply"
              :parentId = "parentId"
              :parentReplyId = "parentReplyId"
              :key="reply.id"

              :showPreview="showPreview"

       >

       </ViewReply>
    </div>

</template>

<script>

    import ViewReply from './ViewReply.vue';


    export default {

        name: 'ViewAllReplies',

        components: {
            "ViewReply": ViewReply,
        },

        props:{
            //repliesList: {default: function (){return []}},

            parentReplyId :{default: null},
            parentId : {default: null},
            showPreview : {default: false},
            reverse: {default: false}
        },

        computed:{

            repliesList(){
                let replies = this.$store.getters.getReplies;

                if (this.reverse) replies = replies.reverse()

                return  replies;
            },

            getChildReplies(){
                let result = [];

                let repliesList = this.repliesList;

                ///console.log("@@@@@@@@@@@ REPLIES LIST", repliesList);

                if ((typeof repliesList !== "undefined")){
                    if (!Array.isArray(repliesList)) repliesList = [repliesList];

                    for (let i=0; i<repliesList.length; i++)
                        if ((repliesList[i] !== null)&&(repliesList[i].parentReplyId == this.parentReplyId)&&(repliesList[i].parentId == this.parentId))
                            result.push(repliesList[i]);

                    if ((result.length === 0)&&(this.parentReplyId==='')) {


                        for (let i = 0; i < repliesList.length; i++){
                            if (repliesList[i].parentId == this.parentId) {

                                let foundParent = false;
                                for (let j = 0; j < repliesList.length; j++)
                                    if (i !== j)
                                        if ((repliesList[j].id == repliesList[i].parentReplyId))
                                            foundParent = true;

                                if (foundParent === false)
                                    result.push(repliesList[i]);

                            }
                        }
                    }

                }

                return result;
            },

        },

        data: function () {
            return {

            }
        }
    }
</script>