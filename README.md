##twitcrypt

This is an experiment in encrypted Twitter communications. Messages are encrypted with AES-256, and packed in Asian characters to make the data safe for transport. Messages can hold up to 144 bytes of data, though with further optimization, message length can probably be extended.

This is still super-early-pre-alpha software, so I would use caution with sensitive data until further reviews are completed - which is to say - DON'T EXPECT IT TO BE SECURE.

###Usage

* `./twitcrypt.rb -dt <tweet url>` - Get's the content of the tweet and decrypts it. *Doesn't work at the moment*
* `./twitcrypt.rb -ed` - This is primarily for testing; displays the encrypted message.
* `./twitcrypt.rb -dd <message - optional>` - This is primarily for testing; decrypts the message.
    
For all options, you will be prompted for the key, so it is not logged to your shell's history. The `-ed` will prompt for the message, and `-dd` will prompt if no message is passed in.

The maximum message size is 138 bytes. The message is 'encoded' into 100 unicode characters.

###Implementation Details

**Encryption:** 256bit AES in CBC mode, performed via the OpenSSL libraries.

**Key Stretching:** PBKDF2 is used on the provided key; SHA1 (for compatibility with older OpenSSL versions) at 25,000 iterations.

**IV:** The IV is generated by creating a 6 byte 'seed' that is stretched via PBKDF2 (SHA1, 25,000 iterations); the seed is stored with the encoded message.

###TODO

Twitter integration - currently there is no integration with Twitter, as I've been focusing on the crypto code first. I'm not sure just how much integration there will be, as Twitter has focused on larger clients, it's become harder for smaller and simpler clients to use the API. So, it's possible that there will always be some copy & paste involved.

###License

Copyright (c) 2013, Adam Caudill <adam@adamcaudill.com>

All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
