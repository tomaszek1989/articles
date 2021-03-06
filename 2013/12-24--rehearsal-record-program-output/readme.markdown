<sub>&#x1F6A8; <strong>Autogenerated!</strong> See <a href="https://github.com/ponyfoo/articles/tree/noindex/contributing.markdown"><code>contributing.markdown</code></a> for details. See also: <a href="https://ponyfoo.com/articles/rehearsal-record-program-output">web version</a>.</sub>

<a href="https://ponyfoo.com/articles/rehearsal-record-program-output"><div><img src="https://i.imgur.com/2GGGGUW.jpg" alt="Rehearsal: Record program output"></div></a>

<h1>Rehearsal: Record program output</h1>

<p><kbd>utility</kbd> <kbd>talks</kbd></p>

<blockquote><p>Persist standard input to a file and keep track of timestamps, then simulate real-time program execution.</p>
</blockquote>

<div><p>Persist standard input to a file and keep track of timestamps, then simulate real-time program execution.</p></div>

<blockquote></blockquote>

<div><p>Ever needed to give a talk on a program and show exactly how the output is going to look like, and such?</p> <p>Maybe you ditched the idea because your program was a bit on the experimental side, and you were afraid it might break, or you were afraid to type the wrong things into the terminal, and boom. <a href="http://net.tutsplus.com/articles/editorials/the-holy-grail-of-conference-talks-live-coding/" target="_blank" rel="noopener noreferrer">Live coding turns into bloodbath</a>, hundreds die.</p></div>

<div><p>I just wrote <a href="https://github.com/bevacqua/rehearsal" target="_blank" rel="noopener noreferrer" aria-label="bevacqua/rehearsal on GitHub">a little thing</a> that can easily read the standard output of a program, and reproduce it at a later time. This sounds pretty simple business, but having it packaged up in a little script, with a simple API, is pretty important.</p> <p>Oh, it also respects delays in the original execution, rather than dumping everything at once.</p> <p>To install it, use <code class="md-code md-code-inline">npm</code>.</p> <pre class="md-code-block"><code class="md-code md-lang-bash">npm i -g rehearsal
</code></pre> <p>Now you can prepare an scenario, suppose you want to give a talk on the awesomeness of <a href="https://github.com/bevacqua/grunt-ec2" target="_blank" rel="noopener noreferrer" aria-label="bevacqua/grunt-ec2 on GitHub">grunt-ec2</a>, which makes lots of requests over the network, and does stuff. It would be great, being able to demonstrate its abilities without the need for an internet connection.</p> <p>You can simply run the command as usual, but pipe its output to <code class="md-code md-code-inline">rehearsal</code>, saving the <code class="md-code md-code-inline">scenario</code> to a file on disk.</p> <pre class="md-code-block"><code class="md-code md-lang-bash">grunt ec2_list --color | rehearsal &gt; scenario
</code></pre> <p>Note that the command is really executed here, we&#x2019;re just redirecting its output, so make sure that that doesn&#x2019;t blow up your repository, or production servers, or anything.</p> <p>I got back a series of encoded streams, persisted in the <code class="md-code md-code-inline">scenario</code> file. I had to use the <code class="md-code md-code-inline">--color</code> argument because <code class="md-code md-code-inline">chalk</code> won&#x2019;t produce any color coding, otherwise.</p> <pre class="md-code-block"><code class="md-code">{&quot;time&quot;:145,&quot;data&quot;:&quot;:base64:MjR0aCAxNzozMjoyNSAtIExvYWRlZCBjb25maWd1cmF0aW9uIGZvciBncnVudCBlbnZpcm9ubWVudAo=&quot;}
{&quot;time&quot;:69,&quot;data&quot;:&quot;:base64:MjR0aCAxNzozMjoyNSAtIGNvbnNvbGUgdHJhbnNwb3J0IGVuYWJsZWQK&quot;}
{&quot;time&quot;:0,&quot;data&quot;:&quot;:base64:MjR0aCAxNzozMjoyNSAtIHB1c2hvdmVyIHRyYW5zcG9ydCBvZmYKMjR0aCAxNzozMjoyNSAtIHBhcGVydHJhaWwgdHJhbnNwb3J0IG9mZgo=&quot;}
{&quot;time&quot;:111,&quot;data&quot;:&quot;:base64:MjR0aCAxNzozMjoyNSAtIExvYWRpbmcgZXh0ZXJuYWwgdGFza3MuLi4=&quot;}
{&quot;time&quot;:1028,&quot;data&quot;:&quot;:base64:ZG9uZSBpbiAxLjI3NjcwNDQ2cwo=&quot;}
{&quot;time&quot;:4,&quot;data&quot;:&quot;:base64:Cg==&quot;}
{&quot;time&quot;:0,&quot;data&quot;:&quot;:base64:G1s0bVJ1bm5pbmcgImVjMl9saXN0IiB0YXNrG1syNG0K&quot;}
{&quot;time&quot;:3,&quot;data&quot;:&quot;:base64:R2V0dGluZyBFQzIgaW5zdGFuY2VzIGZpbHRlcmVkIGJ5IBtbMzZtcnVubmluZxtbMzltIHN0YXRlLi4uCg==&quot;}
{&quot;time&quot;:0,&quot;data&quot;:&quot;:base64:G1s0bRtbMzNtW2NtZF0bWzM5bRtbMjRtIBtbMzVtYXdzIGVjMiBkZXNjcmliZS1pbnN0YW5jZXMgLS1maWx0ZXJzIE5hbWU9aW5zdGFuY2Utc3RhdGUtbmFtZSxWYWx1ZXM9cnVubmluZxtbMzltCg==&quot;}
{&quot;time&quot;:1249,&quot;data&quot;:&quot;:base64:G1szMm0+PiAbWzM5bUZvdW5kIDEgRUMyIEluc3RhbmNlKHMpCg==&quot;}
{&quot;time&quot;:1,&quot;data&quot;:&quot;:base64:G1szNW1pLTRlZTdlMTI4G1szOW0gG1szNW1hbWktYzMwMzYwYWEbWzM5bSAoG1szMm1ydW5uaW5nG1szOW0pIFsbWzM2bXByb2R1Y3Rpb24bWzM5bV0gb24gG1s0bTEwNy4yMC4xOTguMjM5G1syNG0K&quot;}
{&quot;time&quot;:1,&quot;data&quot;:&quot;:base64:Cg==&quot;}
{&quot;time&quot;:0,&quot;data&quot;:&quot;:base64:G1szMm1Eb25lLCB3aXRob3V0IGVycm9ycy4bWzM5bQo=&quot;}
{&quot;time&quot;:1,&quot;data&quot;:&quot;:base64:ChtbNG1FbGFwc2VkIHRpbWUbWzI0bQo=&quot;}
{&quot;time&quot;:1,&quot;data&quot;:&quot;:base64:ZWMyX2xpc3QgIDFzChtbMW1Ub3RhbCAgICAgMXMbWzIybQo=&quot;}
</code></pre> <p>The scenario can be reproduced at any time using the <code class="md-code md-code-inline">reheasal &lt;scenario&gt;</code> command, as shown in the screenshot below.</p> <figure><a href="https://github.com/bevacqua/rehearsal" target="_blank" rel="noopener noreferrer" aria-label="bevacqua/rehearsal on GitHub"><img alt="rehearsal.png" class="" src="https://i.imgur.com/boNkRem.png"></a></figure> <p>If you want to take it up a notch, maybe you&#x2019;d like to create an alias, and then people wouldn&#x2019;t really be able to tell that you were faking it.</p> <pre class="md-code-block"><code class="md-code md-lang-bash"><span class="md-code-built_in">alias</span> realthing=<span class="md-code-string">&quot;rehearsal scenario&quot;</span>
</code></pre> <p>Using spaces in the alias name is a bit tricky, <a href="http://superuser.com/q/105375" target="_blank" rel="noopener noreferrer" aria-label="Bash: Spaces in alias name">but it could be done</a>. By not using an alias, but a function instead.</p></div>
