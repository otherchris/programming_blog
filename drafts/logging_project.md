## 2017-11-29

### Prologue

  At Nodevember I got curious about what's going on with the network
  connection on my machine

  I'm a relative latecomer to software development, and without much formal
  training. As such, until (shockingly) recently, most of what goes on inside
  my MacBook and on the networks it talks on was a mystery to me. That's fairly
  terrifying for a developer starting a career working with state of the art
  systems that push the boundaries of what's possible.

  So I've been cultivating a fantasy of _awareness_. Every event logged, every
  process monitored, every metric visible, every level of functionality tested,
  every deployment scripted, and _absolutely every line of code_ that makes
  these things happen locked into version control.

  Which is, of course, fantasy.

  But it's that great kind of fantasy that makes you want to try something. So
  I got it into my head that I'd like to know everything my computer is doing
  on its ethernet interface. Perhaps there will be surprises, perhaps not, but
  what we have is a goal that we can pursue in a _fantastic_ way.

  **Goal:** Log all activity on the `en0` interface on my laptop.
  **Guideline:** Do everything The Right Way at all times.

#### Getting ready

  First of all, what is a network interface? In this context, it is system
  software that mediates between network hardware (a wireless card in my case)
  and the operating system. Using `ifconfig`, I can see that I have ten network
  interfaces:

  - `lo0`: the loopback interface. This is a pretend network your computer uses
    to talk to itself
  - `gif0`, `stf0`: tunnel interfaces that have something to do with IP4 to IP6
    conversion
  - `en0`: the interface to my wireless network card. This is the intereface we
    will be monitoring
  - `en1`, `en2`: two interfaces for wired networks connected by thunderbolt
  - `bridge0`, `p2p0`, `awdl0`: various Apple specific ways for Aplles toi talk
    to other Apples
  - `pktap0`: ??? but I'm told its nothing to worry about

  The tool we'll use [tcpdump](https://en.wikipedia.org/wiki/Tcpdump). The vast
  configurability of this tool will serve us well a bit down the raod, but at
  first we'll be using mostly default behavior.

  The last thing to do before we start in earnest is to estimate the sizer of
  the data we are going to generate. This will give us an idea of how to chunk
  our data, and what we can expect to be able to accomplosh with the hardware
  we have available.

  Lets log some network activity for 3 minutes and see what we end up with.
  We'll be using another tool, `timelimit`, available on homebrew.

  `timelimit -p -T 0.01 -t 180 tcpdump > current_log`

  Again, we're using default settings for tcpdump, as we change what's being
  logged we'll want to re-estimate the rate at which we accumulate data.

  `-rw-r--r--   1 chriscaragianis staff    251192 Nov 30 08:06 current_log`

  But that's just sitting here watching the clock tick, let's run it again
  while I listen to spotify and answer some slack messages,

  `-rw-r--r--   1 chriscaragianis staff   2563473 Nov 30 08:12 current_log`

  After compressing we have

  `-rw-r--r--   1 chriscaragianis staff    184748 Nov 30 08:16 current_log.zip`

  If we send compressed files, we're looking at an average of 5-6 kbs a minute.


### Act 1 Log everything

  - Step 1: Log the tcpdump, compress, store on remote server, repeat.
    - Rabbit hole: A super quick Elixir endpoint

  - Step 2: Use logstash to read the log files into elasticsearch

- Act 2

  - Step 3: Processing logs with logstash, logstash dev env

  - Step 4: Historical data, what metrics to save?

- Act 3

  - Why write files at all? Piping hot output

-  Epilogue

  - ???

