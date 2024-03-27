# ed-laravel-pusher-private-channel

When you're dealing with a third-party websockets provider, like Pusher, there are two things to consider regarding message security.

First, you want to make sure that only the correct users can see a message. Laravel provides a nice feature called private channels which adds a layer of authorization on top of the websocket channel. Now, a user cannot connect to a channel unless the Laravel app authorizes them.

Second, does it matter to you if Pusher can see the contents your messages as they pass through its servers. This depends on your application. For a hobby project, it might not matter, but if you're in an industry that is subject to strict privacy regulations, it's not enough for you to trust Pusher. You need to go a step further and encrypt the messages.

I recently needed to do this, and I couldn't find anything in the Laravel docs about it. But I knew Pusher supported it, so I dug into the Laravel Echo source code, and I was pleasantly surprised to see that encrypted channels were supported.

There are a few changes needed on both the server and the client to convert a private channel into a private encrypted channel:

![image](https://github.com/GrytsenkoAndrey/ed-laravel-pusher-private-channel/assets/63291871/2ec700fd-ea07-44ec-96fc-fa7a4a2c116e)

With this configuration in place, Laravel and Echo do all the hard work of encrypting and decrypting the messages for you.

Depending on your needs, it might also be worth considering using a self-hosted option like Laravel Reverb to skip the need for message encryption altogether.
