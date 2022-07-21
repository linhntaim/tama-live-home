<template lang="pug">
h1 tama LIVE
button(@click.prevent="startSyncingPrice") Start
button(@click.prevent="stopSyncingPrice") Stop
br
button(@click.prevent="subscribe") Subscribe
button(@click.prevent="unsubscribe") Unsubscribe
</template>

<script>
import {take} from '@/app/support/helpers'
import io from 'socket.io-client'
import {app} from '@/bootstrap/app'

export default {
    // eslint-disable-next-line
    name: 'Home',
    setup() {
        return {
            socket: take(
                io(app.$config.env.VUE_APP_SOCKET_URL, {
                    transports: ['websocket', 'polling'],
                }),
                socket => {
                    socket.on('connected', data => {
                        console.log(data)
                    })
                    socket.on('stream.connected', data => {
                        console.log(data)
                    })
                },
            ),
        }
    },
    data() {
        return {
            interval: {
                id: null,
            },
        }
    },
    mounted() {
        this.socket.on('ws.subscribed', data => {
            console.log(data)
        })
        this.socket.on('symbol.price.fetched', data => {
            console.log(data)
        })
    },
    methods: {
        subscribe() {
            this.socket.emit('subscribe', 'btcusdt@trade')
        },
        unsubscribe() {
            this.socket.emit('unsubscribe', 'btcusdt@trade')
        },
        startSyncingPrice() {
            this.interval.id = setInterval(() => this.socket.emit('symbol.price.fetch', 'BTC'), 1000)
        },
        stopSyncingPrice() {
            if (this.interval.id) {
                clearInterval(this.interval.id)
                this.interval.id = null
            }
        },
    },
}
</script>
