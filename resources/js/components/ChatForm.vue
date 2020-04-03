<template>
    <div class="input-group">
        <input
                id="btn-input"
                type="text"
                name="message"
                class="form-control input-sm"
                placeholder="Type your message here..."
                v-model="newMessage"
                @keyup.enter="sendMessage"
                @keydown="sendTypingEvent"/>

        <span class="input-group-btn">
            <button class="btn btn-primary btn-sm" id="btn-chat" @click="sendMessage">
                Send
            </button>
        </span>
    </div>
</template>

<script>
    export default {
        props: ['user'],

        data() {
            return {
                newMessage: ''
            }
        },

        methods: {
            sendTypingEvent() {
                Echo.join('chat')
                    .whisper('typing', this.user);
            },

            sendMessage() {
                this.$emit('messagesent', {
                    username: this.user.name,
                    message: this.newMessage,
                    isme: true,
                });

                this.newMessage = ''
            },
        },

         watch: {
            newMessage: _.debounce(function() {
              Echo.join('chat')
                    .whisper('stopTyping', this.user);
            }, 2000)
          }
    }
</script>