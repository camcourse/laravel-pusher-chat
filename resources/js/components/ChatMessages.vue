<template>
    <ul class="chat">
        <li class="left clearfix" v-for="(message, key) in messages" :key="key" :class="{'outbound': message.isme}">
            <div class="chat-body clearfix">
                <div class="header">
                    <strong class="primary-font">
                        {{ message.username }}
                    </strong>
                </div>
                <p>
                    {{ message.message }}
                </p>
            </div>
        </li>
    </ul>
</template>

<script>
    export default {
        props: ['messages']
    };
</script>