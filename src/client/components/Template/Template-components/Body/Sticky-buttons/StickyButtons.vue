<template>
    <div >

        <Chat/>

        <NotificationStickyButton v-show="!areNotificationsGranted" :rightOffset="notifcationsStickyButtonRightOffset" />


        <ChatStickyButton :rightOffset="chatStickyButtonRightOffset"/>

    </div>
</template>

<script>

    import NotificationStickyButton from 'modules/notifications/NotificationStickyButton.vue';
    import Chat from 'modules/chat/Chat.vue';
    import ChatStickyButton from 'modules/chat/ChatStickyButton.vue';

    export default{
        name: "StickyButtons",

        data: () => ({

        }),

        computed: {

            notifcationsStickyButtonRightOffset(){
                return 0;
            },

            chatStickyButtonRightOffset (){
                if (this.areNotificationsGranted) return 0;
                else return 50;
            },

            areNotificationsGranted(){
                return this.$store.state.notifications.system.notificationsPermissionGranted;

            }

        },

        components: {
            'Chat': Chat,
            'NotificationStickyButton': NotificationStickyButton,
            'ChatStickyButton': ChatStickyButton,
        }


    }
</script>
